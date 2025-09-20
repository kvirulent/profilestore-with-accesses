# profilestore-with-accesses
roblox-ts bindings for profilestore with an added signal for accesses to the data table

```typescript
// Get a store
import ProfileStore from "@rbxts/profilestore-with-accesses";
import { Players } from "@rbxts/services";
let PlayerStore = ProfileStore.New("PlayerStore", {});

const PROFILE_TEMPLATE = {
  coins: 1000
}

// Start a session and connect to the signal
let profile = this.PlayerStore.StartSessionAsync(...)
profile.accessed.Connect((data: typeof PROFILE_TEMPLATE) => {
    // Callback runs each time profile.Data is indexed or an index is added
    print(data.coins); // Access session data using the table passed to your callback
})
```

Find ProfileStore documentation [here](https://madstudioroblox.github.io/ProfileStore/).

### Important
The package uses `profile.Data` as a proxy table. Underlying data is redirected to `profile._t`. If you want to index `profile.Data` in your callback, you can use the table provided to your callback. 

You cannot modify the data table in your callback. Callbacks are intended to be strictly consumers of data and should not extend data transactions! Ensure any modifications to the table are done before the callback should act on those changes.