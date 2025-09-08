# Sound Effects Directory Structure

This directory contains all sound effects for the Bullet Hell Zombie Game, organized by category for easy management and maintenance.

## Directory Structure

```
sounds/
├── player/          # Player-related sound effects
├── enemies/         # Enemy sound effects (damage, death, special abilities)
├── pickups/         # XP, gold, and item pickup sounds
├── ui/              # User interface sounds
├── minigames/       # Mini-game specific sounds
└── README.md        # This file
```

## Sound Categories

### Player Sounds (`player/`)
- `shoot_01.ogg`, `shoot_02.ogg`, `shoot_03.ogg` - Weapon fire variants
- `melee_01.ogg`, `melee_02.ogg` - Melee attack variants
- `hit_01.ogg`, `hit_02.ogg`, `hit_03.ogg` - Damage taken variants
- `death_01.ogg` - Player death (single for drama)
- `level_up_01.ogg` - Level up sound (single for consistency)
- `upgrade_select.ogg` - Selecting an upgrade

### Enemy Sounds (`enemies/`)
- `zombie_hit_01.ogg`, `zombie_hit_02.ogg` - Zombie damage variants
- `zombie_death_01.ogg`, `zombie_death_02.ogg` - Zombie death variants
- `fast_enemy_hit.ogg` - Fast enemy taking damage
- `tank_hit.ogg` - Tank enemy taking damage
- `boss_roar.ogg` - Boss enemy special sound
- `enemy_spawn.ogg` - Enemy spawning sound

### Pickup Sounds (`pickups/`)
- `xp_pickup_01.ogg`, `xp_pickup_02.ogg`, `xp_pickup_03.ogg` - XP pickup variants
- `gold_pickup_01.ogg`, `gold_pickup_02.ogg` - Gold pickup variants
- `health_pickup.ogg` - Health restoration pickup
- `ammo_pickup.ogg` - Ammunition pickup

### UI Sounds (`ui/`)
- `button_click_01.ogg`, `button_click_02.ogg` - Menu button click variants
- `menu_open.ogg` - Opening menus/panels
- `menu_close.ogg` - Closing menus/panels
- `card_flip.ogg` - Flipping upgrade cards
- `card_select.ogg` - Selecting upgrade cards
- `notification.ogg` - General notifications

### Mini-game Sounds (`minigames/`)
- `slot_machine_spin.ogg` - Slot machine spinning
- `slot_machine_win.ogg` - Slot machine win
- `wheel_spin.ogg` - Wheel of fortune spinning
- `wheel_win.ogg` - Wheel win
- `match_two_correct.ogg` - Match two mini-game correct match
- `match_two_wrong.ogg` - Match two incorrect match

## Sound Variants System

The SoundManager now supports multiple variants of each sound for added variety:

### Automatic Variant Loading
- The system automatically loads variants numbered `_01.wav`, `_02.wav`, etc.
- If no variants exist, it falls back to the base filename
- Up to 10 variants per sound are supported

### Runtime Variations
Each sound can have random variations applied:
- **Pitch**: ±10% variation (configurable)
- **Volume**: ±20% variation (configurable)
- **Rate**: ±5% playback speed variation (configurable)

### Usage Examples
```typescript
// Play random variant with automatic variations
this.soundManager?.playShoot(); // Random shoot_01, shoot_02, or shoot_03 with variations

// Play with custom settings
this.soundManager?.playSoundVariant('player_shoot', {
  volume: 0.8,
  pitch: 1.2,
  skipVariations: true // Disable automatic variations
});

// Play specific variant
this.soundManager?.playSpecificVariant('player_shoot', 1); // Always play shoot_02.ogg
```

## Audio Specifications

### Recommended Format
- **Format**: OGG Vorbis (quality 4-6 recommended)
- **Sample Rate**: 44.1kHz
- **Quality**: 4-6 (VBR)
- **Channels**: Mono (for smaller files) or Stereo (for positional audio)
- **File Size**: Keep under 500KB per sound effect

### Naming Convention
- Use lowercase with underscores
- Include version numbers for variations (e.g., `shoot_01.ogg`, `shoot_02.ogg`)
- Be descriptive but concise
- Group related sounds with consistent prefixes

### Volume Guidelines
- Sound effects should be normalized to -6dB to -12dB peak
- UI sounds: Slightly quieter (-12dB to -18dB)
- Combat sounds: More prominent (-6dB to -9dB)
- Background/ambient sounds: Quietest (-18dB to -24dB)

## Implementation Notes

- All sound files should be placed in their respective category folders
- Consider creating multiple variations of the same sound for variety
- Test sounds in-game to ensure appropriate volume levels
- Use compressed formats (OGG/MP3) for web deployment to reduce bundle size

## Phaser Audio Integration

Sounds will be loaded and managed through Phaser's audio system. Reference the sound files using relative paths from the assets directory.
