---
layout: default
title: C Header Templates
parent: Templates
nav_order: 2
---

# C header file
{: .no_toc }

```
/**
* @file module.h
*
* @brief See the source file.
* 
*/

#ifndef __MODULE_H__
#define __MODULE_H__

#ifdef __cplusplus
extern "C" {
#endif

/* ------------------------------- INCLUDES -------------------------------- */

/* -------------------------------- MACROS --------------------------------- */

/* ------------------------------ DATA TYPES ------------------------------- */

/* --------------------- PUBLIC FUNCTION PROTOTYPES ------------------------ */

/**
 * @brief Description of the function's purpose.
 * 
 */
void public_func(void);

#ifdef __cplusplus
}
#endif

#endif /* __MODULE_H__ */
```

