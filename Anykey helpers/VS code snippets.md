PHP
Снипет для вставки php скобок
```json
    "php tags": {
        "prefix": ["php","<?", "<?php"],
        "body": [ "<?php $1 ?>" ],
        "description": "php tags"
    },

  

    "php echo tags": {
        "prefix": ["php=","<?="],
        "body": [ "<?= $1 ?>" ],
        "description": "php echo tags"
    }
```