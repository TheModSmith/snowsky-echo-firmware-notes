# Research Log

This file tracks new findings that are not already covered in the README.

## Latest Update: Offline image replacement and diff checks

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

extract PNG → edit PNG → convert to `bgr565_be` → patch firmware copy → verify patched resource

### Header and footer unchanged after patching

I compared the original firmware against the custom `entry_0000` replacement firmware.

The custom patch changed 41,416 bytes total:

`cmp -l ECHOV130.IMG ECHOV130_replace_entry0000.IMG | wc -l`

Result:

`41416`

The changed bytes shown by `cmp` fall within the expected `entry_0000` image resource area.

`entry_0000` details:

- Entry: `0000`
- Dimensions: `480x222`
- Format: `bgr565_be`
- Raw size: `213,120` bytes
- Resource offset: `0x009abd78`

I also compared the first 4096 bytes and last 4096 bytes of the original and patched firmware.

Header comparison:

`diff -u checksum_research/original_header_4096.hex checksum_research/patched_header_4096.hex`

Result: no differences.

Footer comparison:

`diff -u checksum_research/original_footer_4096.hex checksum_research/patched_footer_4096.hex`

Result: no differences.

This confirms that the custom PNG replacement did not alter the firmware header, footer, resource table, or file length. The patch only modified image resource data inside the target `entry_0000` range.

### Current conclusion

I have now proven that full-size Echo `ROCK26IMAGERES` image resources can be edited and patched offline, as long as the replacement image keeps the same dimensions and byte size.

The patching process currently changes only the target image resource bytes and does not update any obvious header or footer checksum field.

### New remaining question

The next blocker is no longer image extraction or patching.

The next real research question is whether the firmware/update process will accept a modified image resource.

Before flashing anything, I still need to investigate checksum, signature, footer, update, anti-rollback, and recovery behavior.

The header/footer comparison does not prove that the firmware has no checksum or signature. It only confirms that this patching process did not update any obvious header/footer checksum field.
