# RP2MATH v. 1.0

This is the first release which I am going to call "stable". I will keep the syntax back-compatible with this version for all the minor upgrades of version `1`.

This version **is not back-compatible with `0.1` and `0.2`**, all the RP2MATH function calls have to be rewritten when you upgrade from `0.1` or `0.2`. Unofficial releases which I have distributed via e-mail (`0.3`, `0.4`, `0.5`) **are not back-compatible** either.

The distribution script: [rp2math_1.0.zip][rp2math_1_0_zip].

# System Requirements

- **Operating System**: Windows XP; Windows 7; Windows 8. I have not tested with Windows 10 yet. Let me know if you have!
- **Microsoft Office**: MS Office 2007; MS Office 2010; MS Office 2013.
- **Mathcad**: The only supported version is Mathcad 15.
- **REFPROP**: versions `9.0`, `9.1`.

# Installation

Download and unpack `RP2MATH` script file anywhere you can easily find it later (e.g. your `Documents` folder).

# How to Use RP2MATH

**IMPORTANT: this manual applies to a version `1.0`.**

Add the reference to RP2MATH Mathcad file in the worksheet:

![][mc_reference1]
![][mc_reference2]

As soon as the reference is added, `RP2MATH` functions can be called within the worksheet. The following are few simple examples describing the syntax of `RP2MATH`.

The first example case defines the density of helium at atmospheric pressure (`101325 Pa`) and ambient temperature (`20 C`).

![][mc_example_01]

- First line defines the string variable with the fluid name (`"air"`)
- Two following lines define the pressure and temperature of air at the point of interest. Defined variables `p.1` and `t.1` could be then used as parameters of the `rp2math_density` function.
- Last line calls `rp2math_density` function which returns the density of air at `101325 Pa` and `20 C`.

## Syntax

- The order of inputs is as follows: `fluid name`, `inputs code`, `input 1 value`, `input 2 value`.
- The first and second input parameters of the function correspond to the first and second input codes as per refprop manual. They have to be entered as strings with double quotes `""`.
- The first parameter of the function is the fluid name variable.
- The second parameter of the function is the input code describing fluid properties to be entered as third and forth parameters.
- Next two parameters are input values describing the state of the fluid at the point of interest. The order of these variables should match the input code (i.e. `"PT"` means pressure is the third parameter and temperature is the forth parameter).
- Syntax of `rp2math` scripts is similar to syntax of REFPROP add-in for MS Excel. There are two main differences: the unit system (it's always SI, see the **Units** section below for detailed explanation).

## Fluids

- The names of fluids have to defined as strings. To do so, type the double quote character (quote in the upper-case) **once** and continue typing the name of the fluid inside of the quotes. Mathcad puts both quotes simultaneously when you press the quote key, so there is no need to unquote manually.
- The list of the valid fluid strings is defined in `rp2math_fluids` variable and can be displayed using equal sign anywhere in the worksheet.
- All the names of fluids match their corresponding names with REFPROP add-in for excel.
- The case of the fluid strings does not matter at all, i.e. `"AIR"`, `"air"`, and even `"aIR"` are the same.
- Parameters could be passed to RP2MATH functions both directly or using variables. In order to calculate the property of some fluid only once in you Mathcad documents, it might be easier to use the name of the fluid directly inside of the function:
`enthalpy = rp2math_enthalpy("nitrogen","PT",pressure,temperature)`

![][mc_fluids]

## Input Codes

- Input codes describe the properties to be entered as the third and forth parameters. In the example above, `"PT"` input code indicates that the third parameter is pressure, and the forth parameter is temperature.
- The input code has to be defined as a string. To do so, type the double quote character (quote in the upper-case) **once** and continue typing the input code inside of the quotes. Mathcad puts both quotes simultaneously when you press the quote key, so there is no need to unquote manually.
- The list of possible input codes is defined by `rp2math_inputs` variable and can be displayed using equal sign anywhere in the worksheet.
- All the input codes match their corresponding codes with REFPROP add-in for excel.
- The case of input strings does not matter, i.e. `"PT"` and `"pt"` are the same, however, `"pT"` will not work.

![][mc_inputs]

## Units

- All the fluid properties (pressure, temperature, density, enthalpy, etc) inside of `RP2MATH` functions can be defined with units. Unitless variables are assumed to be in SI system.
- `RP2MATH` **does not** verify the validity of units, i.e. replacement of `Pa` with `kg` would lead to **the exact same result**. That is because `RP2MATH` only rescales all the units to their corresponding SI representations. Since `kg` is a standard SI unit, it is not rescaled after `RP2MATH` function call.
- All the values are returned by `RP2MATH` functions with units. Returned values can be rescaled in a standard Mathcad-way by placing a unit next to the variable.
- Avoid, if possible, working with unitless variables.

![][mc_example_02]

## Functions

- The name of the function defines the property to be returned.
- All the functions start with `rp2math_` and are followed by the name of the property to be calculated.
- The names of properties to be calculated by RP2MATH functions **do not** match their corresponding names with REFPROP add-in for excel. Instead of using one-word names (e.g. `heatofevaporation`) the functions in RP2MATH are defined using underscores (e.g. `rp2math_heat_of_vaporization`).
- The list of the valid function names is defined by `rp2math_functions` variable and can be displayed using equal sign anywhere in the worksheet.

![][mc_functions]

## Saturated conditions and special functions

- Calculations of fluid properties in case if they are fully defined by one variable (i.e. saturated temperature at a given pressure) could have been done using special input codes (e.g. `Pvap`) followed by corresponding value, or special functions (i.e. `rp2math_molar_mass` returns molar mass of the fluid). **It is still necessary to provide all four parameters to the function.** Unused input variables can have any value assigned, but it is recommended to keep it consistent through your spreadsheet for the sake of readability (e.g. `-1` is used in the example below). The reason is that `RP2MATH` functions always expect four input parameters.
- The example below shows the calculation of temperature for saturated liquid nitrogen at atmospheric pressure. `-1` variable is a placeholder to fill the forth parameter.

![][mc_example_03]

- Another example showing how to find a molar mass of helium. There is only one meaningful parameter (name of the fluid). `-1` and `-2` variables are just the placeholders to fill the third and forth parameters, and `"PT"` is used as an input code (it is important to use any **valid** input code in this case).

![][mc_example_04]

# REFPROP installation

In order to use `RP2MATH` functions within Mathcad worksheet, it is necessary to have REFPROP installed and REFPROP add-in file set to work with MS Excel. If REFPROP is already installed (i.e. something like `=density("air","PT","SI",0.1,300)` in excel spreadsheet returns a valid result), ignore this part.

## Installation Process

1. Install REFPROP using the setup launcher with default settings.

    ![][rp_inst]

2. Include the installation path of `REFPROP` to the environment variables:

    - Open `Control Panel`, switch to `Classic View` in Windows XP or to `View by Small icons` in Windows 7 and Windows 8.
    - Click the `System` icon.
    - For Windows 7 and Windows 8: in the left pane, click `Advanced system settings`.
    - On the `Advanced` tab, click `Environment Variables`.

    ![][rp_vars]

    Add the following variables to your `User variables` section:

    | variable   | path (Windows 32-bit)      | path (Windows 64-bit)            |
    |------------|----------------------------|----------------------------------|
    | `path`     | `C:\Program Files\REFPROP` | `C:\Program Files (x86)\REFPROP` |
    | `RPPrefix` | `C:\Program Files\REFPROP` | `C:\Program Files (x86)\REFPROP` |

    If you already have `path` variable in your `User variables` section, simply add an extra path to the end of the line separated by semi-colon sign, i.e. `C:\Windows\system32;C:\Windows;C:\Program Files (x86)\REFPROP`

3. Open `REFPROP.xls` file from default REFPROP installation directory (`C:\Program Files\REFPROP\` for Windows 32-bit, `C:\Program Files (x86)\REFPROP\` for Windows 64-bit).

    ![][rp_xls]

    Go to the `File/Save As…` option in Excel and select `Microsoft Office Excel Add-In` under the `Save as type` section. This will change the extension to `.XLAM`. If the default filename becomes `Copy of REFPROP.xlam` change it to `REFPROP.xlam`. Save the file as `REFPROP.xlam` simply clicking to the `Save` button. Don't change the directory, keep the default path.

    ![][rp_xla]

4. Choose `Add-Ins` tab and click to the `Go...` button.

    In Add-Ins window put a checkmark next to `REFPROP AddIns` and click `OK`.
    
    ![][rp_browse]

5. To verify that you are done with REFPROP installation, open a new Excel document and type `=density("air","PT","SI",0.1,300)` in any cell (or just copy-paste that).

    ![][rp_verif1]

    If everything is OK you should see `1.161299` value when you press ENTER key. The value shows density of air in `kg/m^3` at `0.1MPa` pressure and `300K` temperature.

    ![][rp_verif2]

[rp2math_1_0_zip]: ../../raw/master/rp2math_v1.0.zip
[mc_reference1]: ./images/mc_reference1.png
[mc_reference2]: ./images/mc_reference2.png
[mc_fluids]: ./images/mc_fluids.png
[mc_functions]: ./images/mc_functions.png
[mc_inputs]: ./images/mc_inputs.png
[mc_example_01]: ./images/mc_example_01.png
[mc_example_02]: ./images/mc_example_02.png
[mc_example_03]: ./images/mc_example_03.png
[mc_example_04]: ./images/mc_example_04.png
[rp_inst]: ./images/rp_inst.png
[rp_xls]: ./images/rp_xls.png
[rp_xla]: ./images/rp_xla.png
[rp_browse]: ./images/rp_browse.png
[rp_verif1]: ./images/rp_verif1.png
[rp_verif2]: ./images/rp_verif2.png
[rp_vars]: ./images/rp_vars.png
