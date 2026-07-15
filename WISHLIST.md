# Flowing Fluids Wishlist

This document collects possible future directions for Flowing Fluids. It is an
idea bank, not a committed roadmap. Features should remain configurable and
should not compromise the mod's finite-volume behavior, world safety, or server
performance.

## Design guardrails

- Conserve fluid volume unless an explicit source or sink is involved.
- Keep simulation server-authoritative and multiplayer-safe.
- Process active fluid frontiers instead of scanning whole chunks.
- Never force-load chunks; defer work safely at unloaded boundaries.
- Put hard budgets on fluid, heat, pressure, and gas work per tick.
- Preserve worlds when a feature is disabled or the mod is removed where
  practical.
- Prefer tags and public APIs over hard-coded compatibility rules.
- Keep loader-specific hooks thin so core behavior stays consistent.

## Thermal water and steam

- Tag-driven heat sources such as fire, campfires, lava, magma, and heated
  machine blocks.
- Ambient, warm, hot, and boiling water states without attaching a block entity
  to every water block.
- Boiling that consumes real water levels instead of creating free effects.
- Steam particles, bubbling sounds, scalding damage, and cooking for items or
  entities in boiling water.
- A lightweight first version where steam is an effect, followed by persistent
  volumetric steam only if it can be simulated safely.
- Condensation on cold surfaces and in cold biomes, returning steam to finite
  water.
- Boilers, geysers, pressure release, and steam bursts.
- Optional humidity and weather coupling: evaporation contributes to local
  rain, while rain refills exposed water.
- Heat exchangers and cooling loops for automation-focused modpacks.

## Fluid machines

- Redstone-controllable pumps with visible throughput and finite intake.
- Pipes that respect fluid type, volume, throughput, elevation, and pressure.
- Valves, check valves, drains, filters, and redstone floodgates.
- Grates that let fluids pass while blocking entities and items.
- Tanks, reservoirs, gauges, and redstone fluid-level sensors.
- Boilers, condensers, steam engines, turbines, and safety valves.
- A sponge press or dryer for emptying absorbed water into a tank or pipe.
- Mechanical piston pumps that remain useful without another technology mod.
- First-class integration with Create and generic loader fluid-transfer APIs.

## Hydraulics and simulation

- Hydrostatic head so elevated reservoirs can drive pipes and machines.
- Communicating vessels, siphons, and pressure-aware upward flow.
- Configurable natural-water behavior ranging from protected oceans to
  catastrophic lake-to-cave drainage.
- Better rules for partial waterlogging and differently shaped block volumes.
- Deterministic settling across chunk boundaries and save/reload cycles.
- A debug overlay for fluid level, flow direction, active cells, pressure, and
  per-tick simulation cost.
- GameTests for mass conservation, dams, waterfalls, pumps, chunk boundaries,
  boiling, condensation, and machine round-trips.

## World and survival systems

- Springs, wells, aquifers, and configurable renewable-water sources.
- Irrigation where farmland consumes finite water over time.
- Dams, canals, aqueducts, sluices, and water-powered machinery.
- Hot springs, geysers, seasonal freezing, and biome-aware evaporation.
- Optional finite groundwater and soil saturation.
- Controlled flood events and mapmaker-friendly flood scenarios.
- Water quality, filtration, or salinity as optional compatibility hooks rather
  than mandatory core mechanics.

## FiniteLiquid-inspired ideas

- Classic pipes, pumps, redstone grates, and neighboring-water sensors.
- Reusable sponges that can be squeezed or dried instead of deleting water.
- Heated metal blocks that boil nearby water and can cook or harm entities.
- Optional underground methane pockets with ventilation, ignition, and
  explosion behavior.
- Optional oil, quicksand, or other finite fluids implemented through the same
  public simulation API.

## Suggested implementation order

1. Thermal effects: tagged heat sources, boiling, finite evaporation, particles,
   damage, and cooking without persistent steam.
2. Utility machines: pumps, pipes, valves, grates, tanks, gauges, and sponge
   recovery.
3. Pressure systems: hydrostatic head, boilers, persistent steam, condensers,
   and turbines.
4. Environmental systems: aquifers, irrigation, humidity, rain, groundwater,
   and advanced gases.
