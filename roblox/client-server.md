# Client–server trust boundary
Versions: Roblox engine <VERSION>
Last verified: <DATE>

- The client is controlled by exploiters. Anything it sends is untrusted input.
- Every `RemoteEvent` / `RemoteFunction` handler validates **on the server**: types, ranges, rate, ownership, and cooldowns.
- Never trust positions, amounts, prices, damage, targets, or IDs sent by the client. The server works them out from its own state.
- The server owns money, inventory, and progression. The client only *requests*.
- Don't call `RemoteFunction:InvokeClient` from the server. Use `RemoteEvent:FireClient`. Docs: if the client doesn't return, "the server yields forever", and client errors and disconnects throw on the server ([ref](https://create.roblox.com/docs/reference/engine/classes/RemoteFunction)). TODO(verify): confirm this is our rule.
- Any new remote → human review (see [[agents/server-scripter/card]]).
- Our remote naming: see [[studio]].
