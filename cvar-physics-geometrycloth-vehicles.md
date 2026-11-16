# Geometry Collection, Cloth, and Modular Vehicle physics CVars

This guide covers all currently uncovered registered `p.GeometryCollection.*` (8), `p.Cloth.*` (8), and `p.ModularVehicle.*` (6) names in the supplied community registry. The groups relate to destructible geometry, cloth creation/teleport behavior, and modular vehicle simulation. Community help and snapshot values are separated from exact-name Epic UE 5.9 references; the registry does not establish the game’s capture build or engine revision.

Build evidence is from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may be a read, comparison, or write; references to a CVar `var` object can be setup code. None of this proves the setting is consumed in a match or that the mod loader accepts an override. No live query or gameplay test was performed.

## Geometry Collection

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.GeometryCollection.AlwaysGenerateConnectionGraph` | bool (`ref`) | `false` | `false` | When enabled, always  generate the cluster's connection graph instead of using the rest collection stored one - Note: this should only be used for troubleshooting.[def: false] *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.AlwaysGenerateGTCollisionForClusters` | bool (`ref`) | `true` | `true` | When enabled, always generate a game thread side collision for clusters.[def: true] *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.AreaBasedDamageThresholdMode` | int32 (`ref`) | `0` | `0` | Area based damage threshold computation mode (0: sum of areas \| 1: max of areas \| 2: min of areas \| 3: average of areas) [def: 0] *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.EnabledNestedChildTransformUpdates` | bool (`ref`) | `true` | `true` | Enable updates for driven, disabled, child bodies. Used for line trace results against geometry collections.[def: true] *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.MemeoryOpt` | bool (`ref`) | `true` | `—` | No explanatory help or exact Epic reference was found; behavior remains unresolved. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.ParallelBufferPhysicsResults` | bool (`ref`) | `false` | `—` | If true, buffer physics results in parallelly. *(source: community help)* | 6 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.RestRemoveParticleHandle` | bool (`ref`) | `true` | `—` | When enabled, always  rest remove Particle handle *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.GeometryCollection.XRUpdateTolerance` | float (`ref`) | `0.0001` | `—` | Tolerance to detect if a XR has changed has changed when syncing PT to GT *(source: community help)* | 6 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |

## Cloth system

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.Cloth.ClothColliderMaxShapeNum` | int32 (`var`) | `6` | `—` | Cloth Collider Max Shape Num. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.DefaultClothingSimulationFactoryClass` | FString (`var`) | `—` | `ChaosClothingSimulationFactory` | The class name of the default clothing simulation factory. Known providers are: ChaosClothingSimulationFactory *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.MaxDeltaTimeTeleportMultiplier` | float (`var`) | `1.5` | `1.5` | A multiplier of the MaxPhysicsDelta time at which we will automatically just teleport cloth to its new location  default: 1.5 *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.ParallelCreateClothActor` | bool (`var`) | `true` | `—` | Parallel Create Cloth Actor.  Default: true. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.ResetAfterTeleport` | bool (`var`) | `true` | `true` | Require p.Cloth.TeleportOverride. Reset the clothing after moving the clothing position (called teleport).  Default: true. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.TeleportDistanceThreshold` | float (`var`) | `300` | `300` | Require p.Cloth.TeleportOverride. Conduct teleportation if the character's movement is greater than this threshold in 1 frame.  Zero or negative values will skip the check.  Default: 300. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.TeleportOverride` | bool (`var`) | `false` | `false` | Force console variable teleport override values over skeletal mesh properties.  Default: false. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |
| `p.Cloth.TeleportRotationThreshold` | float (`var`) | `0` | `0` | Require p.Cloth.TeleportOverride. Rotation threshold in degrees, ranging from 0 to 180.  Conduct teleportation if the character's rotation is greater than this threshold in 1 frame.  Zero or negative values will skip the check.  Default 0. *(source: community help)* | CVar-object setup/address references only; no `ref_rva` value-access field exists for this `var`. |

## Modular Vehicle

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.ModularVehicle.DisableAllSimulationAfterDestruction.Enable` | bool (`ref`) | `false` | `—` | Enable/Disable whole vehicle simulation after destruction has occured. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.ModularVehicle.DumpModuleTreeStructure.Enabled` | bool (`ref`) | `false` | `—` | Enable/Disable logging of module tree structure every time there is a change. *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.ModularVehicle.EnableCustomInputQuantization` | bool (`ref`) | `false` | `—` | Enable/Disable Custom Input Quantization info. Default: false *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.ModularVehicle.EnableInputSendingTypeInfo` | bool (`ref`) | `true` | `—` | Enable/Disable Input sending type info. Default: true *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.ModularVehicle.NetworkData.Enable` | bool (`ref`) | `true` | `—` | Enable/Disable additional module network data. *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |
| `p.ModularVehicle.SuspensionConstraint.Enabled` | bool (`ref`) | `true` | `—` | Enable/Disable suspension constraint falling back to simple forces when constraint disabled (requires restart). *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime control flow were not traced. |

## Interpretation limits

- The descriptions cover collision graph generation, game-thread collision, area-based damage threshold modes, transforms, cloth simulation factories, teleport reset thresholds, time-step handling, and modular-vehicle simulation/network controls. Settings marked with no description remain unknown beyond their registry name and static address matches.
- Snapshot values are captured values, not recommendations. Epic defaults are exact-name upstream context, not confirmed Marvel Rivals defaults.
- Physics, networking, and solver changes can affect simulation behavior. The static evidence does not prove any setting is safe to change during a live match or that a startup override is accepted.

For related simulation settings, see [Rigid Body Node and Chaos Cloth CVars](cvar-physics-rigidbody-chaoscloth.md) and the [community CVar registry](cvar-community-registry.md). Build inventory and scan scope are summarized in [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).

