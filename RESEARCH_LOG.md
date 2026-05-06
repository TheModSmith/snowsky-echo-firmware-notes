# Research Log

This file tracks new findings that are not already covered in the README.

## Latest Update: Offline image replacement works

### Offline same-size resource swap works

I created a patched firmware copy where one existing resource was copied over another:

entry_0001 → entry_0000

Result:

Firmware length unchanged: yes  
Resource table unchanged: yes  
Patched file reparses: yes  
Target now equals source: yes  
Only target range changed: yes  

This confirms that the resource offsets are correct and same-size raw image replacement can be done without altering the table or firmware length.

### Custom PNG replacement works offline

I edited `entry_0000_480x222_off_0x009abd78_bgr565_be.png` and patched it back into a firmware copy.

The replacement tool converted the edited PNG back into raw `bgr565_be` and patched only `entry_0000`.

Result:

Firmware length unchanged: yes  
Resource table unchanged: yes  
Patched file reparses: yes  
Target equals PNG encode: yes  
Only target range changed: yes  

### Patched preview confirmed

I confirmed the generated preview image showed the edited `TEST EDIT` graphic correctly after conversion back to `bgr565_be`.

This confirms the full offline image-editing chain:

extract PNG → edit PNG → convert to bgr565_be → patch firmware copy → verify patched resource

### Current conclusion

I have now proven that full-size Echo `ROCK26IMAGERES` image resources can be edited and patched offline, as long as the replacement image keeps the same dimensions and byte size.

### New remaining question

The next blocker is no longer image extraction or patching.

The next real research question is whether the firmware/update process will accept a modified image resource.

Before flashing anything, I still need to investigate checksum, signature, footer, update, and recovery behavior.
