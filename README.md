# Brother's Modding Library

This mod countains various parts and features used most notably in the Faction Expansion: Tortoises mod, as well as any other of our upcoming mods. You will find below a non-exhaustive list of the mod's content. Feel free to use it for your own mods!

# Documentation

## New Conversation Parts
The mod countains several new parts that can be called in any .xml conversation. You will find in the mod's files a sample conversation countaining various example of how said parts can be used, but here is a quick rundown.

### `Brothers_RequirePart`

Although the game already has the IfHavePart predicate that only displays a dialogue option if you have the relevant part (be it mutation or skill), the Brothers_RequirePart conversation part will actually display the dialogue option greyed out if you lack the relevant part, as well as the needed part in brackets.

```xml
<part Name="Brothers_RequirePart" Part="Carapace" Render="Mutation: Carapace" />
```
### `Brothers_RequireStat`

Similarly to the game's RequireReputation or this mod's Brothers_RequirePart, Brothers_RequireStat lets you display dialogue options that require a minimum attribute to select. If that minimum is not met, the option will be greyed out.

```xml
<part Name="Brothers_RequireStat" Stat="Ego" Value="20" />
```

### `Brothers_ModifyReputation`

This part allows for manipulation of reputations through dialogue options. Up to two separate reputations can be either increased or decreased with a single dialogue option.

```xml
<part Name="Brothers_ModifyReputation" Faction="Cats" Value="100" Faction2="Dogs" Value2="-100" Shown="True" />
