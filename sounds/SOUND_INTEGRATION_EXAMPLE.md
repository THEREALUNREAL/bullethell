# Sound Effects Integration Examples

This document shows how to integrate the sound effects into your game code using the SoundManager.

## Basic Usage

The SoundManager is automatically initialized in MainScene and can be accessed via `this.soundManager`.

### Player Actions (Now with Variants!)

```typescript
// When player shoots - plays random shoot variant with pitch/volume variations
this.soundManager?.playShoot();

// When player performs melee attack - plays random melee variant
this.soundManager?.playMelee();

// When player takes damage - plays random hit variant
this.soundManager?.playPlayerHit();

// When player dies - consistent sound (no variations for drama)
this.soundManager?.playPlayerDeath();

// When player levels up - consistent sound (no variations)
this.soundManager?.playLevelUp();
```

### Enemy Actions (Now with Variants!)

```typescript
// When enemy takes damage - plays random hit variant
this.soundManager?.playEnemyHit();

// When enemy dies - plays random death variant
this.soundManager?.playEnemyDeath();
```

### Pickups (Now with Variants!)

```typescript
// When collecting XP - plays random pickup variant
this.soundManager?.playXpPickup();

// When collecting gold - plays random pickup variant
this.soundManager?.playGoldPickup();
```

### UI Interactions (Now with Variants!)

```typescript
// When clicking buttons - subtle pitch and volume variations
this.soundManager?.playButtonClick();

// When flipping upgrade cards - consistent timing with slight volume variation
this.soundManager?.playCardFlip();

// When selecting an upgrade - consistent sound
this.soundManager?.playCardSelect();
```

### Mini-games

```typescript
// When spinning slot machine - consistent sound
this.soundManager?.playSlotSpin();
```

## Advanced Variant Usage

### Custom Sound Variations

```typescript
// Play with custom settings
this.soundManager?.playSoundVariant('player_shoot', {
  volume: 0.8,        // 80% volume
  pitch: 1.2,         // 20% higher pitch
  skipVariations: true // Disable automatic random variations
});

// Play with only volume variation
this.soundManager?.playSoundVariant('enemy_hit', {
  volume: Phaser.Math.FloatBetween(0.8, 1.2),
  skipVariations: true
});
```

### Specific Variant Selection

```typescript
// Always play the second variant
this.soundManager?.playSpecificVariant('player_shoot', 1); // plays shoot_02.ogg

// Always play the first variant with custom pitch
this.soundManager?.playSpecificVariant('player_hit', 0, {
  pitch: 0.9,  // Lower pitch
  volume: 1.5  // Louder
});
```

### Configure Variation Ranges

```typescript
// Customize variation ranges for more or less variation
this.soundManager?.configureVariations({
  pitchRange: { min: 0.8, max: 1.2 },    // ±20% pitch variation
  volumeRange: { min: 0.7, max: 1.3 },   // ±30% volume variation
  rateRange: { min: 0.9, max: 1.1 }      // ±10% rate variation
});
```

### Check Available Variants

```typescript
// Get number of variants for a sound
const shootVariants = this.soundManager?.getVariantCount('player_shoot'); // Returns 3

// Get current variation settings
const settings = this.soundManager?.getVariationSettings();
console.log(settings.pitchRange); // { min: 0.9, max: 1.1 }
```

## Advanced Usage

### Volume Control

```typescript
// Adjust master volume (0.0 to 1.0)
this.soundManager?.setMasterVolume(0.8);

// Adjust SFX volume specifically
this.soundManager?.setSfxVolume(0.9);

// Mute/unmute all sounds
this.soundManager?.setMuted(true);
```

### Custom Sound Playback

```typescript
// Play any sound with custom volume
this.soundManager?.playSound('player_shoot', 0.5);

// Get current volume settings
const masterVol = this.soundManager?.getMasterVolume();
const sfxVol = this.soundManager?.getSfxVolume();
```

## Integration Points

### In Character.ts (Player Actions)

```typescript
// In shooting method
shoot() {
  // ... existing shoot logic ...
  this.scene.soundManager?.playShoot();
}

// In takeDamage method
takeDamage(damage: number) {
  // ... existing damage logic ...
  this.scene.soundManager?.playPlayerHit();
}
```

### In Enemy Classes

```typescript
// In takeDamage method
takeDamage(damage: number) {
  // ... existing damage logic ...
  this.scene.soundManager?.playEnemyHit();
}

// In destroy method
destroy() {
  this.scene.soundManager?.playEnemyDeath();
  super.destroy();
}
```

### In Pickup Collection

```typescript
// In pickup collection logic
collectPickup(pickup: Pickup) {
  if (pickup instanceof XPPickup) {
    this.scene.soundManager?.playXpPickup();
  } else if (pickup instanceof GoldPickup) {
    this.scene.soundManager?.playGoldPickup();
  }
  // ... rest of collection logic ...
}
```

### In UI Components

```typescript
// In button click handlers
handleButtonClick() {
  this.scene.soundManager?.playButtonClick();
  // ... button logic ...
}

// In card flip animations
flipCard() {
  this.scene.soundManager?.playCardFlip();
  // ... flip animation ...
}
```

## File Structure Reminder

```
sounds/
├── player/
│   ├── shoot_01.wav
│   ├── melee_01.wav
│   ├── hit_01.wav
│   ├── death_01.wav
│   └── level_up_01.wav
├── enemies/
│   ├── zombie_hit.wav
│   ├── zombie_death.wav
│   └── enemy_spawn.wav
├── pickups/
│   ├── xp_pickup.wav
│   ├── gold_pickup.wav
│   └── health_pickup.wav
├── ui/
│   ├── button_click.wav
│   ├── card_flip.wav
│   └── card_select.wav
└── minigames/
    ├── slot_machine_spin.wav
    ├── wheel_spin.wav
    └── minigame_win.wav
```

## Next Steps

1. **Add Sound Files**: Place your sound files in the appropriate directories following the naming convention
2. **Test Integration**: Add sound calls to key game events as shown above
3. **Volume Balancing**: Adjust volume levels in the SoundManager for optimal audio experience
4. **Additional Sounds**: Add more sound variations for variety (shoot_02.ogg, hit_02.ogg, etc.)

## Notes

- Sounds will only play if the audio files exist in the specified paths
- The SoundManager gracefully handles missing sound files by logging warnings
- Volume settings are persisted and affect all sound playback
- Consider adding sound toggles to your game's settings menu
