Follow: https://gist.github.com/azvoleff/f8f06d22a8a4d89401e09d6607a5ecc4
Important under way to:
- in `$ sudo nano /etc/postgresql/9.3/main/pg_hba.conf` set `peer` to `md5 in:
`# Database administrative login by Unix domain socket`
`local   all             postgres                                md5`
- set the "postgres" users´ password with postgres=# ALTER USER postgres PASSWORD 'myPassword';
- Give access without key pair (low security) -https://stackoverflow.com/questions/6119774/ssh-to-aws-instance-without-key-pairs (bottum comment)
