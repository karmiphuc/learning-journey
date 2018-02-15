These directives can help to secure PHP sessions better:

```apache
<IfModule mod_php5.c>

  # Separate each project's sessions.
  php_value session.use_only_cookies off
  php_value session.save_path "YOUR_WEBROOT/sessions"
  
  # Better session ID generation (cannot guarantee 100% unique, though)
  php_value session.entropy_file "/dev/urandom"
  php_value session.entropy_length 512
  
</IfModule>
```
