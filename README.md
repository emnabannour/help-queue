# Help Queue

A queue students use to ask for help during practical sessions (Laravel, TP1 to TP3).

## Requirements

- PHP 8.4 or newer, Composer and Node.js (for example with Laravel Herd)
- Git

## Installation

```bash
git clone https://github.com/emnabannour/help-queue help-queue
cd help-queue
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
composer run dev
```

Then open http://localhost:8000.

- The database file is not in Git: `php artisan migrate --seed` offers to create it, answer **yes**.
- In the Windows Command Prompt (cmd), use `copy .env.example .env` instead of `cp`.

## Troubleshooting

- `composer install` fails with an SSL certificate error: your antivirus may be
  scanning HTTPS connections (for example Avast). Turn off its HTTPS scanning.
- `php -v` shows a version lower than 8.4: another PHP (for example Laragon) comes
  first in your Path. Put Herd's folder first.
  
