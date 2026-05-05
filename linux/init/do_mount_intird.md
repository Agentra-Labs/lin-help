

## initrd_load.c (initrd handling logic)

### Purpose
Handles loading of the initial RAM disk (initrd) during early boot.

---

## Global Variables

- `initrd_start`, `initrd_end`  
  Memory range where initrd is located.

- `initrd_below_start_ok`  
  Flag controlling placement of initrd in memory.

- `mount_initrd`  
  Controls whether initrd should be mounted (default: enabled).

- `phys_initrd_start`  
  Physical start address of initrd.

- `phys_initrd_size`  
  Size of initrd in memory.

---

## Boot Parameters

### `noinitrd`
```c
__setup("noinitrd", no_initrd);
````

**Description:**
Disables initrd loading.

**Behavior:**

* Sets `mount_initrd = 0`
* Prints warning (deprecated)

---

### `initrdmem=<start,size>`

```c
early_param("initrdmem", early_initrdmem);
```

**Description:**
Specifies initrd memory location manually.

**Behavior:**

* Parses memory address and size
* Sets:

  * `phys_initrd_start`
  * `phys_initrd_size`

---

### `initrd=<...>`

```c
early_param("initrd", early_initrd);
```

**Description:**
Alias for `initrdmem`

---

## Key Function

### `initrd_load()`

```c
void __init initrd_load(void)
```

**Purpose:**
Loads initrd into a RAM device during boot.

---

### Execution Flow

1. Check if initrd mounting is enabled

   ```c
   if (mount_initrd)
   ```

2. Create RAM device

   ```c
   create_dev("/dev/ram", Root_RAM0);
   ```

3. Load initrd into RAM

   ```c
   rd_load_image()
   ```

4. If successful:

   * Prints deprecation warning
   * Suggests using initramfs instead

5. Cleanup temporary file

   ```c
   init_unlink("/initrd.image");
   ```

---

## Notes

* Initrd is considered **deprecated**
* Kernel recommends:

  * initramfs (preferred)
  * `/sys/firmware/initrd` (fallback)

---

## Relevance

* Part of early boot process
* Runs before full userspace is available
* Bridges kernel → userspace transition (legacy path)

---

## When To Look Here

* Boot issues involving initrd
* Custom initrd memory configuration
* Debugging early userspace loading


