---
description: >-
  These queries return the number of users in the audience. If you'd like to get
  the list of user IDs in the audience instead, then remove the outermost
  COUNT() function, e.g., COUNT(DISTINCT user_id) -
---

# Bigquery - Sample queries for audiences based

Source: [https://support.google.com/firebase/answer/9037342?hl=en](https://support.google.com/firebase/answer/9037342?hl=en)

### N-day active users <a id="ndayactives"></a>

```sql
/**
 * Builds an audience of N-Day Active Users.
 *
 * N-day active users = users who have logged at least one user_engagement
 * event in the last N days.
*/
SELECT
  COUNT(DISTINCT user_id) AS n_day_active_users_count
FROM
  -- PLEASE REPLACE WITH YOUR TABLE NAME.
  `YOUR_TABLE.events_*`
WHERE
  event_name = 'user_engagement'
  -- Pick events in the last N = 20 days.
  AND event_timestamp >
      UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP, INTERVAL 20 DAY))
  -- PLEASE REPLACE WITH YOUR DESIRED DATE RANGE.
  AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131';

```

### N-day inactive users <a id="ndayinactives"></a>

```sql
/**
 * Builds an audience of N-Day Inactive Users.
 *
 * N-Day inactive users = users in the last M days who have not logged a
 *   user_engagement event in the last N days where M > N.
 */
SELECT
  COUNT(DISTINCT MDaysUsers.user_id) AS n_day_inactive_users_count
FROM
  (
    SELECT
      user_id
    FROM
      /* PLEASE REPLACE WITH YOUR TABLE NAME */
      `YOUR_TABLE.events_*`
    WHERE
      event_name = 'user_engagement'
      /* Has engaged in last M = 7 days */
      AND event_timestamp >
          UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY))
      /* PLEASE REPLACE WITH YOUR DESIRED DATE RANGE */
      AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131'
  ) AS MDaysUsers
-- EXCEPT ALL is not yet implemented in BigQuery. Use LEFT JOIN in the interim.
LEFT JOIN
  (
    SELECT
      user_id
    FROM
      /* PLEASE REPLACE WITH YOUR TABLE NAME */
      `YOUR_TABLE.events_*`
    WHERE
      event_name = 'user_engagement'
      /* Has engaged in last N = 2 days */
      AND event_timestamp >
          UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 2 DAY))
      /* PLEASE REPLACE WITH YOUR DESIRED DATE RANGE */
      AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131'
  ) AS NDaysUsers
  ON MDaysUsers.user_id = NDaysUsers.user_id
WHERE
  NDaysUsers.user_id IS NULL;
```

### Frequently active users <a id="frequentactives"></a>

```sql
/**
 * Builds an audience of Frequently Active Users.
 *
 * Frequently Active Users = users who have logged at least once
 * 'user_engagement' event on N of the last M days where M > N.
 */
SELECT
  COUNT(DISTINCT user_id) AS frequent_active_users_count
FROM
  (
    SELECT
      user_id,
      COUNT(DISTINCT event_date)
    FROM
      -- PLEASE REPLACE WITH YOUR TABLE NAME.
      `YOUR_TABLE.events_*`
    WHERE
      event_name = 'user_engagement'
      -- User engagement in the last M = 10 days.
      AND event_timestamp >
          UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 10 DAY))
      -- PLEASE REPLACE YOUR DESIRED DATE RANGE.  For optimal performance
      -- the _TABLE_SUFFIX range should match the INTERVAL value above.
      AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131'
    GROUP BY 1
    -- Having engaged in at least N = 4 days.
    HAVING COUNT(event_date) >= 4
  );

```

### Highly active users <a id="highactives"></a>

```sql
/**
 * Builds an audience of Highly Active Users.
 *
 * Highly Active Users = users who have been active for more than N minutes
 * in the last M days where M > N.
*/
SELECT
  COUNT(DISTINCT user_id) AS high_active_users_count
FROM
  (
    SELECT
      user_id,
      event_params.key,
      SUM(event_params.value.int_value)
    FROM
      -- PLEASE REPLACE WITH YOUR TABLE NAME.
      `YOUR_TABLE.events_*` AS T
    CROSS JOIN
      T.event_params
    WHERE
      event_name = 'user_engagement'
      -- User engagement in the last M = 10 days.
      AND event_timestamp >
          UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 10 DAY))
      AND event_params.key = 'engagement_time_msec'
      -- PLEASE REPLACE YOUR DESIRED DATE RANGE.
      AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131'
    GROUP BY 1, 2
    HAVING
      -- Having engaged for more than N = 0.1 minutes.
      SUM(event_params.value.int_value) > 0.1 * 60 * 1000000
  );

```

### Acquired users <a id="acquired"></a>

```sql
/**
 * Builds an audience of Acquired Users.
 *
 * Acquired Users = users who were acquired via some Source/Medium/Campaign.
 */
SELECT
  COUNT(DISTINCT user_id) AS acquired_users_count
FROM
  -- PLEASE REPLACE WITH YOUR TABLE NAME.
  `YOUR_TABLE.events_*`
WHERE
  traffic_source.source = 'google'
  AND traffic_source.medium = 'cpc'
  AND traffic_source.name = 'VTA-Test-Android'
  -- PLEASE REPLACE YOUR DESIRED DATE RANGE.
  AND _TABLE_SUFFIX BETWEEN '20180521' AND '20240131';
```

### Cohorts with filters <a id="cohorts"></a>

```sql
/**
 * Builds an audience composed of users acquired last week
 * through Google campaigns, i.e., cohorts with filters.
 *
 * Cohort is defined as users acquired last week, i.e. between 7 - 14
 * days ago. The cohort filter is for users acquired through a direct
 * campaign.
 */
SELECT
  COUNT(DISTINCT user_id) AS users_acquired_through_google_count
FROM
  -- PLEASE REPLACE WITH YOUR TABLE NAME.
  `YOUR_TABLE.events_*`
WHERE
  event_name = 'first_open'
  -- Cohort: opened app 1-2 weeks ago. One week of cohort, aka. weekly.
  AND event_timestamp >
      UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 14 DAY))
  AND event_timestamp <
      UNIX_MICROS(TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY))
  -- Cohort filter: users acquired through 'google' source.
  AND traffic_source.source = 'google'
  -- PLEASE REPLACE YOUR DESIRED DATE RANGE.
  AND _TABLE_SUFFIX BETWEEN '20180501' AND '20240131';
```

