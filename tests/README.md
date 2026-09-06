# Balance checks for the Reaches

Two test classes that came out of the engine repository with this content, because what they assert
is true of *this world* rather than of the engine.

| File | What it holds the content to |
|---|---|
| `WeaponBalanceTests.cs` | Every weapon declares its own dice, no two share a stat line, each shop line beats the one below it, and the epic tiers rank Blade, Warden, Hallow, Adept |
| `QuestRewardBalanceTests.cs` | Every quest pays a sensible share of a level, and the deepest realm really does scale experience |

They read the merged bundle off disk and evaluate it with the engine's own arithmetic — the same
reason `check-bundle` compiles against the server rather than transcribing its rules. That is also
why they are not runnable on their own: **they need the engine checked out beside this repository**,
and how that is wired is the open question in `docs/CONTENT-SPLIT.md` §6 over there.

## Why they are not simply gone

The rules that generalise already moved into `BundleValidator`, so `check-bundle` enforces them for
any world: every mob a spawner places can be hit and can hit back, and every quest offer carries
exactly one marker sitting inside its sentence. What is left here does not generalise. "The epic
tiers rank Blade, Warden, Hallow, Adept" is a claim about `epic-warden-1` and its siblings; asserted
in the engine it would fail against every other world, and asserting it nowhere would mean nobody
notices when a retune quietly inverts the order.

Until they are wired up, they are a record of what the numbers were meant to say. Deleting them
would lose that, and it is not recoverable from the bundles themselves — the bundles are the
numbers, not the intent behind them.
