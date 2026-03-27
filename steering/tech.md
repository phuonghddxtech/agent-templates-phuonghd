# Tech Stack

## Backend

- **Framework**: Laravel 9.x (PHP 8.0+)
- **Database**: MySQL 5.7
- **Cache/Queue**: Redis
- **Queue Driver**: Database-based with Supervisor workers
- **Authentication**: Laravel Sanctum (token-based API auth)
- **Key Packages**:
  - `maatwebsite/excel` — Excel import/export
  - `barryvdh/laravel-dompdf` — PDF generation (payslips)
  - `intervention/image` — Image processing
  - `spatie/laravel-activitylog` — Audit logging
  - `aws/aws-sdk-php` + `league/flysystem-aws-s3-v3` — S3 file storage
  - `symfony/mailgun-mailer`, `wildbit/swiftmailer-postmark` — Email providers

## Frontend

- **Framework**: Vue.js 2.6.10
- **State Management**: Vuex 3.x
- **i18n**: vuex-i18n
- **Build Tool**: Laravel Mix 6.0 (Webpack)
- **CSS**: Sass/SCSS → compiled to `css/`
- **UI Libraries**: Bootstrap 4, CoreUI 2, FullCalendar 5, Chart.js 2, Mapbox GL 2, Dropzone 5

## Infrastructure

- **Containerization**: Docker (Alpine Linux 3.17, Nginx 1.22, PHP 8.1-FPM)
- **Process Manager**: Supervisor (manages Nginx, PHP-FPM, cron, queue workers)
- **Docker Compose Services**:
  - `hrm_app` — main app (Nginx + PHP-FPM)
  - `hrm_db` — MySQL 5.7
  - `hrm_phpmyadmin` — DB admin UI
  - `hrm_bpo_redis` — Redis

## Common Commands

### Docker
```bash
docker-compose up -d          # Start all services
docker-compose down           # Stop all services
docker-compose exec hrm_app bash  # Shell into app container
```

### Laravel (run inside container or with correct PHP path)
```bash
php artisan migrate           # Run migrations
php artisan migrate:fresh --seed  # Reset DB and seed
php artisan db:seed           # Run seeders
php artisan queue:work        # Start queue worker
php artisan tinker            # Interactive REPL
php artisan make:controller   # Scaffold controller
php artisan make:model        # Scaffold model
php artisan make:migration    # Create migration
```

### Frontend Assets
```bash
npm run dev       # Build assets (development)
npm run prod      # Build assets (production, minified + versioned)
npm run watch     # Watch for changes and rebuild
```

### Testing
```bash
# Backend (PHPUnit)
./vendor/bin/phpunit

# Frontend (Jest)
npx jest --runInBand
```

### Code Style
```bash
# PHP CS Fixer
./vendor/bin/php-cs-fixer fix src/
```

## Environment

Copy `.env.example` to `.env` in `src/`. Key variables:
- `APP_URL`, `APP_ENV`, `APP_KEY`
- `DB_*` — MySQL connection
- `REDIS_*` — Redis connection
- `MAIL_*` — Email configuration
- `AWS_*` — S3 storage (optional)
- `FILESYSTEM_DRIVER` — `local` or `s3`
