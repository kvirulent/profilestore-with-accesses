# profilestore-with-accesses
roblox-ts bindings for profilestore with an added signal for accesses to the data table

```ts
// Get a store
import ProfileStore from "@rbxts/profilestore-with-accesses";
import { Players } from "@rbxts/services";
let PlayerStore = ProfileStore.New("PlayerStore", {});

// Start a session and connect to the signal
let profile = this.PlayerStore.StartSessionAsync(...)
profile.accessed.Connect(() => {
    // Callback runs each time profile.Data is indexed or an index is added
})
```

### Important
The package uses `profile.Data` as a proxy table. Underlying data is actually redirected to a table `profile._t`. If you want to index `profile.Data` in the accessed callback, use `profile._t` in order to avoid an infinite loop, as indexing `profile.Data` within the callback will still cause the signal to fire.