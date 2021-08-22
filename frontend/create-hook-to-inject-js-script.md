# Create hook to inject JS script

```jsx
import { useEffect } from "react"

export const useInjectScript = (src: string) =>
  useEffect(() => {
    // @ts-ignore
    if (window.__custom_injected__) return
    // @ts-ignore
    window.__custom_injected__ = true

    const script = document.createElement("script")
    script.src = src
    script.defer = true

    const onScriptError = () => script.remove()
    script.addEventListener("error", onScriptError)

    document.body.appendChild(script)
  }, [])
```

```jsx
import { useInjectScript } from './useInjectScript'

 const Component = () => {
  useInjectScript('https://duyet.net/x/lib.js')
  
  return (...)
 } 
```

