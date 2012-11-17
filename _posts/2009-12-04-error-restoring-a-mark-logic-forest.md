---
author: Rob
title: Error restoring a MarkLogic forest
excerpt:
layout: post
---

After it spent about 2 hours restoring a forest I got an annoying but slightly amusing error:

    500 Internal Server Error
    
    XDMP-EXTIME: xdmp:sleep(3000) -- Time limit exceeded
    in /forest-backup-go.xqy, on line 56 [0.9-ml]

Now what do I do? Try again and cross fingers this time?

And why is restore not async in the admin ui? Backup is..

This is just the first forest, there’s another 4 to go. Not what I need on Friday afternoon :(

Rant over.

UPDATE… Rookie mistake believing the error message meant the restore had failed – turns out it has worked!