# Flappy Bird Clone

```
    ___      ___
   (o o)    (o o)
  (  V  )  (  V  )
 /|  |  |\/|  |  |\
  |  |  |  |  |  |
     FLAPPY BIRD
```

A classic Flappy Bird clone built with Godot 4.5, featuring smooth gameplay mechanics and a winter-themed aesthetic.

## Overview

This project is a faithful recreation of the popular mobile game Flappy Bird. Players control a plane navigating through obstacles by tapping to make it jump, with the goal of achieving the highest score possible.

## Features

- **Intuitive Controls**: Simple one-button gameplay (Space or Mouse Click)
- **Score Tracking**: Persistent high score system with local save
- **Medal System**: Earn Bronze, Silver, or Gold medals based on performance
  - Bronze: 0-9 points
  - Silver: 10-19 points
  - Gold: 20+ points
- **Winter Theme**: Snow-themed obstacles and ground textures
- **Sound Effects**: Jump, score, hit, and game over audio feedback
- **Smooth Physics**: Realistic gravity and rotation mechanics

## Game Architecture

### Core Components

#### Main Scene (`scenes/main/main.gd`)
- Game orchestration and state management
- Score tracking and high score persistence
- Signal coordination between game components
- Save/load system using `user://score.save`

#### Player (`scenes/player/player.gd`)
- Character physics with gravity (1000.0) and jump force (400.0)
- Input handling for jump mechanics
- Rotation animation based on velocity
- Movement state management

#### Obstacle System (`scenes/obstacle/obstacle.gd` & `scenes/extra/spawner.gd`)
- Dynamic obstacle spawning at randomized heights
- Collision detection for crashes
- Score area detection for point increments
- Automatic cleanup when obstacles leave screen

#### Ground (`scenes/ground/ground.gd`)
- Infinite scrolling ground animation
- Seamless texture looping
- Player collision detection
- Movement control (150 pixels/second)

#### Game UI (`scenes/game_ui/game_ui.gd`)
- Start menu overlay
- Real-time score display
- Game over menu with medal presentation
- Restart functionality

## Code Review

### Strengths

1. **Clean Architecture**: Well-organized scene structure with clear separation of concerns
2. **Signal-Based Communication**: Proper use of Godot signals for decoupled component interaction
3. **Type Safety**: Uses class names and type hints (`class_name`, `-> void`, etc.)
4. **Resource Management**: Proper use of `@onready` for node references
5. **Performance**: Efficient obstacle cleanup with `queue_free()` when off-screen

### Technical Highlights

- **Physics**: Uses `CharacterBody2D` with proper delta-time scaling
- **Viewport Awareness**: Obstacles spawn relative to viewport dimensions
- **Functional Programming**: Uses `filter()` with lambda for obstacle iteration
- **Export Variables**: Configurable gameplay parameters (gravity, speed, jump force)

### Minor Observations

- Typo in `spawner.gd:16` - `half_hight` should be `half_height`
- Input handling uses `is_action_pressed()` which allows continuous input - works well for the game feel

## Project Structure

```
flappy-bird-clone/
├── scenes/
│   ├── main/           # Main game controller
│   ├── player/         # Player plane character
│   ├── obstacle/       # Obstacle prefab
│   ├── extra/          # Spawner system
│   ├── ground/         # Scrolling ground
│   └── game_ui/        # UI overlays
├── FlappyBirdAssets/
│   ├── Audio/          # Sound effects (sfx_hit, sfx_die, sfx_point, sfx_wing)
│   ├── Sprites/        # Visual assets (planes, UI, obstacles, background)
│   └── Fonts/          # Score font
└── project.godot       # Godot project configuration
```

## Technical Specifications

- **Engine**: Godot 4.5
- **Rendering**: Mobile renderer
- **Resolution**: 480x854 (portrait mobile)
- **Physics**: Custom gravity simulation with CharacterBody2D
- **Platform Target**: Mobile (with desktop support)

## Controls

- **Space** or **Left Mouse Button**: Jump/Flap

## Installation & Running

1. Install [Godot 4.5](https://godotengine.org/download) or later
2. Clone this repository
3. Open the project in Godot
4. Press F5 or click "Run Project"

## Development Notes

The game uses Godot's built-in physics engine with custom gravity implementation. The spawner uses a timer-based system to create obstacles at regular intervals, with randomized vertical positioning to create varied gameplay challenges.

High scores are saved locally using Godot's `FileAccess` API, storing a 32-bit integer in the user data directory.

## License

This is an educational project created as part of a Godot game development course.

---

**Made with Godot Engine**
