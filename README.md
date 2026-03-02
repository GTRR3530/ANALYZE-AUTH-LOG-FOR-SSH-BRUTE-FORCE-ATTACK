Analyze Auth Logs for SSH Brute Force

On the Attacker Machine:

hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://TARGET-IP
This will attempt multiple password guesses for user root on the SSH port.

Ensure SSH is enabled on the target:

sudo systemctl status ssh
🔍 Step 2: Detection and Analysis – Analyze Auth Logs
Check for failed login attempts:

sudo grep "Failed password" /var/log/auth.log
Find usernames tried:

sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr
Watch live log activity:

sudo tail -f /var/log/auth.log
