---
title: "Finding out which process runs on a certain port using powershell"
date: 2022-05-29T20:38:00+02:00
draft: false
---

At one point I was wondering which process was running on port `3000` because I wanted to debug another application (which also uses) that port. So I ran the following command.

<!--more-->

```ps
Get-Process -Id (Get-NetTCPConnection -LocalPort 3000).OwningProcess
```

This resulted in the following list.

```
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    597      28    37052      31844     103,34  34028   6 com.docker.backend
    127      11     1528       1728       1,97  22220   6 wslhost
```

Which made me realize I was still runing something in docker :D