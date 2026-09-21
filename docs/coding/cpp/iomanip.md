---
title: iomanip and std::hex
---

# iomanip and std::hex

### `std::hex`

**it sets the numeric output format of `std::cout` to hexadecimal**. This means that any integers printed to `std::cout` after this statement will be displayed in base 16 (hexadecimal) instead of the default base 10 (decimal).

??? note "Code"
    
    ```cpp
    #include <iostream>
    
    int main() {
        int num = 255;
    
        std::cout << "Decimal: " << num << std::endl; // Default: decimal format
        std::cout << std::hex;
        std::cout << "Hexadecimal: " << num << std::endl; // Now prints in hex
        std::cout << std::dec;
        std::cout << "Back to Decimal: " << num << std::endl; // Resets to decimal
    
        return 0;
    }
    ```
    
    ```powershell
    //Output
    
    Decimal: 255
    Hexadecimal: ff
    Back to Decimal: 255
    ```

## Practice Questions

??? question "1. What does std::hex do?"

    It sets the numeric output format of `std::cout` to hexadecimal, so integers printed afterward appear in base 16.

??? question "2. How do you go back to decimal?"

    Send `std::dec` to `std::cout`.

??? question "3. What does the example print for 255 in hex?"

    `ff`.
