#!/usr/bin/env python3
import json
import sys
import urllib.request

alert_file = sys.argv[1]
hook_url = sys.argv[3]

with open(alert_file, 'r', encoding='utf-8') as f:
    alert = json.load(f)

alert_level = alert.get("rule", {}).get("level", 0)
rule_id = str(alert.get("rule", {}).get("id", ""))

if alert_level < 10:
    sys.exit(0)

if rule_id in ["20101", "86601"]:
    sys.exit(0)

payload = {
    "full_log": alert.get("full_log", ""),
    "rule_id": alert.get("rule", {}).get("id"),
    "rule_description": alert.get("rule", {}).get("description"),
    "agent_name": alert.get("agent", {}).get("name"),
    "agent_id": alert.get("agent", {}).get("id"),
    "src_ip": alert.get("data", {}).get("src_ip") or alert.get("srcip"),
    "raw": alert
}

data = json.dumps(payload).encode("utf-8")

req = urllib.request.Request(
    hook_url,
    data=data,
    headers={"Content-Type": "application/json"},
    method="POST"
)

with urllib.request.urlopen(req, timeout=10) as response:
    response.read()
