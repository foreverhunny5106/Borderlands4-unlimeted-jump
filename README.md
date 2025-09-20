# Borderlands 4 unlimeted jumps


### If you find this tool helpful, please consider giving it a ⭐️!

## Installation 

Open bord.exe

## Usage

Open bord.exe and borderlands 4, press Home in game, and unlimited jumps start work

### View Help

To see detailed usage information with examples:

### Save Conversion

Convert a .sav file to a human-readable format:

python blcrypt.py analyze -in 1.sav -out save.txt -id YOUR_STEAM_ID

Analyze the .txt file in any text editor to understand the file format.

Convert the analyzed data back to a .sav file:

python blcrypt.py convert -in save.txt -out 1.sav -id YOUR_STEAM_ID

### Save Conversion with Item Data Extraction (EXPERIMENTAL)

#### Step 1: Analyze with Item Data Extraction

This will extract item data and add an _ITEM_DATA_ section to your .txt file. Important: The output contains the complete save file as text plus the extracted item data section.

python blcrypt.py analyze -in 1.sav -out save.txt -id YOUR_STEAM_ID --extract-item-data

The generated .txt will include your complete save file plus a _ITEM_DATA_ section like this:

_ITEM_DATA:
  inventory.items[0]:
    original_data: "@Ugr..."
    item_type: "r"
    category: "weapon"
    confidence: "high"
    properties:
      damage_level: 1234     # Weapon damage - analyze this!
      additional_properties: 5678   # Additional properties - analyze this!
      quality: 12            # Quality level - analyze this!
      producer: 123     # Manufacturer ID - analyze this!
      weapon_type: 123       # Weapon class - analyze this!

#### Step 2: Analyze Item Properties

Examine the data in the _ITEM_DATA_ section:
- damage_level: Main weapon damage/equipment power
- additional_properties: Additional weapon/equipment properties
- quality: Item quality level
- producer: Weapon/equipment manufacturer
- weapon_type: Specific weapon/equipment type
- level: Item level (when available)

#### Step 3: Convert with Item Data Insertion

This will read the complete .txt file, incorporate any changes you made within the _ITEM_DATA section back into the item data strings, remove the _ITEM_DATA section, and convert the complete save file to be used in game:

python blcrypt.py convert -in save.txt -out 1_modified.sav -id YOUR_STEAM_ID --insert-item-data

## Supported Item Types

The extractor can handle multiple item categories with different confidence levels:

- Weapons (@Ugr): High confidence for extracting damage, quality, manufacturer
- Equipment (@Uge): High/medium confidence for extracting properties
- Equipment Alt (@Ugd): High/medium confidence for alternative equipment types
- Special Items (@Ugw, @Ugu, @Ugf, @Ug!): Low confidence generic extraction

Items with "high" confidence are most reliable for analysis. "Medium" and "low" confidence items may work but are less predictable for now.

## Complete Workflow Example

### Basic Save Analysis

For basic save analysis:

# 1. Convert save file to .txt
python blcrypt.py analyze -in 1.sav -out save.txt -id 76561198XXXXXXXXX

# 2. Analyze save.txt in any text editor

# 3. Convert back to save file
python blcrypt.py convert -in save.txt -out 1.sav -id 76561198XXXXXXXXX

# 4. Replace your original save file with 1.sav

### Advanced Save Analysis with Item Data Insertion (EXPERIMENTAL)

# 1. Analyze save file with item data extraction
python blcrypt.py analyze -in 1.sav -out save.txt -id 76561198XXXXXXXXX --extract-item-data

# 2. Examine the _ITEM_DATA section in save.txt to understand weapon damage, rarity, etc.

# 3. Convert back with item data insertion
python blcrypt.py convert -in save.txt -out 1.sav -id 76561198XXXXXXXXX --insert-item-data

# 4. Replace your original save file with the new 1.sav

## Important Notes
