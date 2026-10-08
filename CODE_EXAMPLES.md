# Code examples — AFTER

> **Exemple illustratif Godot/GDScript**, écrit pour expliquer la séparation simulation / présentation. Ce n'est pas un extrait certifié du projet privé.

## Une machine transforme un état, pas une animation

```gdscript
class_name RecyclerRule
extends RefCounted

static func can_process(stock: Dictionary) -> bool:
    return int(stock.get("polymer", 0)) >= 2

static func process(stock: Dictionary) -> Dictionary:
    var next_stock: Dictionary = stock.duplicate(true)
    if not can_process(next_stock):
        return next_stock

    next_stock["polymer"] = int(next_stock["polymer"]) - 2
    next_stock["filament"] = int(next_stock.get("filament", 0)) + 1
    return next_stock
```

Une scène Godot peut afficher une animation après la transition, mais n'est pas responsable de modifier elle-même le stock.

## Test indépendant du rendu

```gdscript
func test_recycler_transition() -> void:
    var initial := {"polymer": 2, "filament": 0}
    var result := RecyclerRule.process(initial)

    assert(result["polymer"] == 0)
    assert(result["filament"] == 1)
    assert(initial["polymer"] == 2)
```

**Point d'architecture :** logique de transition isolée, entrée non mutée, test sans scène graphique. Les règles réelles, la concurrence et la persistance ne sont pas démontrées par cet exemple.
