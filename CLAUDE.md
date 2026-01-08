# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Chaos Yut (카오스 윷놀이)** is a Korean traditional board game (Yut Nori) implementation in Unreal Engine 5.6. This is an educational project developed over 7 weekly assignments, using Blueprint-only development (no C++ code).

- **Engine**: Unreal Engine 5.6
- **Development Model**: Blueprint-only (no C++ source code)
- **Main Level**: `Content/ChaosYut.umap`
- **Current Status**: Week 7 completed (January 2026)

## Working with this Project

### Opening the Project

1. Ensure Unreal Engine 5.6 is installed
2. Double-click `Chaos_Yut.uproject` to open in Unreal Editor
3. The main level will load automatically, or navigate to `Content/ChaosYut.umap`

### Project Structure

Since this is a Blueprint-only project, all logic resides in `.uasset` files which can only be edited within Unreal Editor:

```
Content/
├── BluePrint/           # Core game logic Blueprints
│   ├── BP_YutBoard      # Main game board controller
│   ├── BP_RoadBase      # Individual board positions
│   ├── BP_YutPiece      # Player game pieces
│   ├── ST_YutData       # Yut outcome data structure
│   └── DT_YutData       # Yut outcomes DataTable
├── UI/                  # Game framework and UI
│   ├── GM_Yut           # GameMode (game initialization)
│   ├── PC_Yut           # PlayerController (core game logic)
│   └── WBP_YutButton    # Main UI widget for yut rolling
├── Material/            # Visual materials
├── Mesh/               # Static meshes
└── ChaosYut.umap       # Main game level
```

### Blueprint Assets Cannot Be Modified via Text

**Important**: Blueprint files (`.uasset`) are binary assets that can only be edited in Unreal Editor. Claude Code cannot directly modify Blueprint logic. When asked to make changes to game logic:

1. Provide clear instructions on which Blueprint to open
2. Specify which function/event graph to modify
3. Describe the Blueprint node changes needed
4. Reference specific variables or functions by name

Example response format:
```
To add this feature, open BP_YutPiece in Unreal Editor:
1. Open the Event Graph
2. Find the MoveToRoad function
3. Add a new Timeline node before the SetActorLocation call
4. Configure the timeline to animate movement over 0.5 seconds
```

## Architecture Overview

### Game Framework Layer

- **GM_Yut** (GameMode): Initializes game, sets default player pawn to BP_PlayerStartView
- **PC_Yut** (PlayerController): Central game controller managing all game flow
  - `SelectYutPiece(BP_YutPiece)`: Selects a piece and shows selection marker
  - `DeselectYutPiece()`: Deselects current piece
  - `MoveSelectedPieceToRoad(BP_RoadBase)`: Moves selected piece to destination
  - `RollYut()`: Executes probability-based yut roll using DT_YutData
- **BP_PlayerStartView** (Pawn): Camera-only pawn positioned above game board

### Game Logic Layer

**BP_YutBoard** (182KB - most complex Blueprint)
- Central game board controller
- Manages array of BP_RoadBase child actors
- Links roads together via Prev/Next relationships
- Acts as hub connecting pieces, roads, and movement logic

**BP_RoadBase** (67KB) and Road Variants
- Base class for all board positions
- Handles click detection for piece movement destinations
- Stores references to previous/next roads for navigation
- Variants:
  - `BP_BranchRoad`: Fork points where paths split
  - `BP_Junction`: Convergence points where paths merge
  - `BP_MergeRoad`: Shortcut/diagonal paths

**BP_YutPiece** (88KB)
- Individual game piece ("말" - horse)
- `MoveToRoad(BP_RoadBase)`: Relocates piece to specified road
- `SetSelectedMarkVisibility(bool)`: Toggles selection marker
- Contains hierarchical selection marker components

### Data-Driven Game Rules

**ST_YutData** (Structure): Defines schema for yut outcomes
- `YutName` (Text): Outcome name (도, 개, 걸, 윷, 모, 뒷도)
- `Chance` (double): Probability weight

**DT_YutData** (DataTable): Contains all 6 possible yut outcomes with probabilities
- Referenced by PC_Yut's RollYut() function
- Enables rule changes without modifying Blueprint logic

### UI Layer

**WBP_YutButton** (188KB)
- Main game interface widget
- Two-state button: "Roll" → "Pick Up" → "Roll"
- Pre-roll animation: Cycles through outcomes before displaying result
- Integrated with PC_Yut's RollYut() function

## Key Game Flow

1. **Piece Selection**: Player clicks BP_YutPiece → OnClick → PC_Yut.SelectYutPiece()
2. **Piece Movement**: Player clicks BP_RoadBase → OnClick → PC_Yut.MoveSelectedPieceToRoad()
3. **Yut Rolling**: Player clicks WBP_YutButton → PC_Yut.RollYut() → Result from DT_YutData

## Development Patterns

### Event-Driven Architecture
All player interactions use OnClickEvent binding:
- Pieces and roads detect clicks locally
- GetPlayerController → Cast to PC_Yut
- Centralized game logic execution in PlayerController

### Data-Driven Design
Game rules live in DataTables, not hard-coded in Blueprints:
- Add new yut outcomes by editing DT_YutData
- Change probabilities without touching Blueprint logic
- Structure (ST_YutData) defines the contract

### Component Hierarchy
- BP_YutBoard contains BP_RoadBase child actors
- BP_YutPiece contains selection marker components
- Enables visual organization and iteration

## Git Workflow

This project uses weekly milestone commits:
- Branch: `main`
- Commit pattern: "YYMMDD - Week N 과제" (e.g., "260103 - 7주차 과제")
- All development happens on main branch

### Common Git Commands

```bash
# Check current status
git status

# Commit weekly progress
git add Content/ Config/
git commit -m "YYMMDD - N주차 과제"

# View recent commits
git log --oneline -5
```

## Important Notes for AI Assistants

1. **No Direct Code Editing**: Blueprint `.uasset` files are binary. Provide Unreal Editor instructions instead of code changes.

2. **Testing Changes**: Changes must be tested by:
   - Opening project in Unreal Editor
   - Playing in editor (PIE) from ChaosYut.umap
   - Clicking pieces to select, roads to move, button to roll

3. **Asset References**: When referring to Blueprints, use full names:
   - Correct: "Open BP_YutPiece in Content/BluePrint/"
   - Incorrect: "Edit the piece script"

4. **Weekly Progression**: This is a learning project. Respect the incremental development:
   - Week 1-2: Core actors and movement
   - Week 3-4: UI and game data
   - Week 5: Yut rolling mechanics
   - Week 6-7: Selection and player flow

5. **No C++ Code**: This project intentionally uses Blueprint-only development. Do not suggest C++ implementations unless specifically requested.

## Reference: Key Blueprint Files by Size

Size indicates complexity/logic density:
- BP_YutBoard: 182KB (board management)
- WBP_YutButton: 188KB (UI logic)
- BP_YutPiece: 88KB (piece behavior)
- PC_Yut: 71KB (game controller)
- BP_RoadBase: 67KB (road logic)

## Planning Documents

The `규칙문서/` directory contains project planning materials:
- `아이디어 기획 구체화.pdf`: Original game design document
- `2025.11.17_카오스윷놀이맵.xlsx`: Game board layout specifications

These documents are in Korean and define the game rules and board structure.

## Custom Agents and Skills

This project includes custom Claude Code agents and skills to streamline development workflow.

### Custom Agents (.claude/agents/)

Specialized agents for complex, multi-step tasks:

#### 1. **blueprint-architecture-planner**
- **Purpose**: Design Blueprint architecture for new features
- **When to use**: Adding new game systems, planning major features
- **Outputs**: Architecture diagrams, implementation plans, Blueprint modification lists
- **Example**: "Design a turn-based system for Team A and Team B"

#### 2. **game-mechanics-debugger**
- **Purpose**: Diagnose and fix Blueprint bugs and logic errors
- **When to use**: Unexpected behavior, crashes, logic failures
- **Outputs**: Root cause analysis, step-by-step fixes, prevention recommendations
- **Example**: "Pieces aren't moving when I click roads"

#### 3. **feature-implementation-guide**
- **Purpose**: Provide step-by-step Unreal Editor instructions for implementing features
- **When to use**: Ready to implement a designed feature
- **Outputs**: Detailed node-by-node Blueprint instructions, test scenarios
- **Example**: "Guide me through adding movement animation to pieces"

#### 4. **blueprint-refactoring-advisor**
- **Purpose**: Analyze code quality and suggest refactoring improvements
- **When to use**: Blueprints getting complex, maintainability concerns
- **Outputs**: Code smell detection, refactoring proposals, optimization suggestions
- **Example**: "BP_YutBoard is 182KB, how can I improve it?"

#### 5. **unreal-learning-assistant**
- **Purpose**: Teach UE5 concepts, nodes, mechanisms, and data structures
- **When to use**: Learning new UE5 features, choosing between approaches
- **Outputs**: Beginner to advanced explanations, comparisons, project-specific examples
- **Example**: "How does Timeline work? Should I use Array or TMap for this?"

### Custom Skills (.claude/skills/)

Quick, single-purpose operations:

#### 1. **weekly-commit**
- **Purpose**: Automate weekly assignment commits with consistent format
- **Usage**: `/weekly-commit 8` or "주간 커밋해줘 (8주차)"
- **Action**: Stages Content/ and Config/, commits as "YYMMDD - N주차 과제"

#### 2. **find-blueprint**
- **Purpose**: Quickly locate Blueprint files and show metadata
- **Usage**: `/find-blueprint YutPiece` or "BP_YutPiece 어디있어?"
- **Output**: File path, size, last modified date

#### 3. **check-references**
- **Purpose**: Analyze Blueprint dependencies and references
- **Usage**: `/check-references BP_RoadBase`
- **Output**: Dependency diagram, which Blueprints use/are used by target

#### 4. **show-structure**
- **Purpose**: Display current project status snapshot
- **Usage**: `/show-structure` or "프로젝트 상태 보여줘"
- **Output**: Git status, recent commits, Blueprint sizes, directory structure

#### 5. **update-docs**
- **Purpose**: Automatically update CLAUDE.md with project changes
- **Usage**: `/update-docs` or "문서 업데이트해줘"
- **Action**: Detects new Blueprints, updates architecture section, refreshes file sizes

#### 6. **blueprint-template**
- **Purpose**: Provide standardized guides for creating new Blueprints
- **Usage**: `/blueprint-template Actor` or "새 Widget Blueprint 만들려고"
- **Output**: Creation checklist, naming conventions, integration patterns

### Using Agents and Skills

**Invoke agents explicitly**:
```
Use the blueprint-architecture-planner agent to design a turn system
Ask the unreal-learning-assistant about Event Dispatchers
```

**Skills activate automatically** based on context or can be called directly:
```
/weekly-commit 8
/show-structure
```

### Workflow Example

Typical feature development flow:

```
1. Design Phase
   └─ blueprint-architecture-planner agent
      → Architecture design, Blueprint list

2. Learning Phase (if needed)
   └─ unreal-learning-assistant agent
      → Understand required UE5 concepts

3. Implementation Phase
   └─ feature-implementation-guide agent
      → Step-by-step Unreal Editor instructions

4. Debugging Phase (if issues)
   └─ game-mechanics-debugger agent
      → Root cause analysis, fixes

5. Quality Phase
   └─ blueprint-refactoring-advisor agent
      → Code quality improvements

6. Documentation Phase
   └─ /update-docs skill
      → Sync CLAUDE.md with changes

7. Commit Phase
   └─ /weekly-commit skill
      → Consistent Git commit
```
