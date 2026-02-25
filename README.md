# CMPM147_Affix_Generator

Pokémon Nature Generator

A Tiny Weighted Generator with Meta Bias and Synergy Rules

Overview

This project recreates and extends the Pokémon “Nature” system as a weighted procedural generator.

In mainline Pokémon games, each Nature modifies a creature’s stats by increasing one stat by 10% and decreasing another by 10%. There are 25 possible combinations across five stats (Atk, Def, SpA, SpD, Spe), including 5 neutral natures that produce no change.

This generator reconstructs that 5×5 matrix structure and adds weighted bias and build-based synergy constraints to demonstrate controlled procedural variation rather than pure randomness.

Generative Logic (Procedural Idea)

The system is built from a structured matrix:

5 stats × 5 stats = 25 possible nature combinations

If up == down, the nature is neutral

Otherwise:

Up stat × 1.1

Down stat × 0.9

Instead of selecting uniformly at random, the generator uses weighted sampling based on:

Meta Focus Bias

Build Tag Synergy Rules

Optional discouragement of neutral natures

This ensures output variation is intentional and parameter-driven.

Control & Parameters

The generator includes the following meaningful parameters:

1. Meta Focus (Distribution Bias)

Changes the probability of certain stat boosts appearing.

Physical → Strongly biases toward +Atk, discourages -Atk

Special → Biases toward +SpA

Speed → Biases toward +Spe

Bulky → Biases toward +Def / +SpD

Neutral → No bias

This parameter noticeably changes the frequency distribution of boosted stats.

2. Build Tag (Synergy Constraints) – Optional Challenge B

Implements affix-style compatibility logic:

Physical Sweeper

Cannot lower Atk

Prefers +Atk or +Spe

Special Sweeper

Cannot lower SpA

Prefers +SpA or +Spe

Tank

Cannot lower Def or SpD

Prefers defensive boosts

Mixed

Discourages lowering Atk or SpA

These rules function similarly to affix synergy systems in item generators, preventing or encouraging specific combinations.

3. Allow Neutral Toggle

Controls whether the five neutral natures are included in the sampling pool.

Disabling this removes stat-neutral outcomes from the distribution.

Output Evidence

The interface supports:

Generating 10+ sample outputs

Running 100-trial statistical simulations

The statistical output shows:

Frequency of each boosted stat

Frequency of each lowered stat

Neutral occurrence rate

Changing Meta Focus clearly shifts the distribution. For example:

Under Physical, +Atk appears significantly more often.

Under Speed, +Spe dominates the UP frequency.

Under Bulky, defensive boosts become more common.

This demonstrates controlled procedural generation rather than uniform randomness.

Optional Challenge Implemented

B – Affix Synergy Rules

BuildTag constraints prevent incompatible stat combinations, similar to how item affixes in RPG systems cannot coexist.

Example:

A Physical Sweeper will never receive a nature that lowers Attack.

A Tank will never receive a nature that lowers Defense.

This ensures structural coherence between system intent and generated output.

Reflection

One surprising aspect was how quickly weight adjustments could dominate the distribution. Even small multipliers (e.g., ×2) significantly skew results over 100 trials.

Another challenge was preventing invalid combinations from eliminating too many possible outcomes. Hard bans (weight = 0) require careful balancing to avoid over-constraining the system.

If expanded further, I would connect this generator to Pokémon base stat spreads or move types, allowing synergy rules to dynamically adapt to a specific creature rather than a generic build tag. This would make the system closer to a full procedural build recommender.

Technical Notes

Implemented in vanilla JavaScript

Uses weighted random selection

Matrix-based stat generation

UI built with simple HTML/CSS

All logic runs client-side in browser
