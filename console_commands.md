# PHP Console Commands

- `php -v` - show version of PHP
- `php --ini` - show paths to loaded *.ini files of PHP
- `php -m` - show installed PHP Modules
- Start development server:
  - `php -S 127.0.0.1:8000` - current dir is root dir
  - `php -S 127.0.0.1:8000 -t web/ web/front.php` - `-t` - sets root dir, `web/front.php` - router script
