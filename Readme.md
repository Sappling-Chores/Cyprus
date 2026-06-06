<div align="center">

![logo](Assets\Edit_Gallery\Cyprus_logo1.png)



<img src="Assets\Render_Gallery\Render19.png" width="400px">



</div>



Cyprus is 60 % mechanical split keyboard designed by Mohammad Sarfaraz aka Sappling.

### Features:

* This keyboard is handwired so its very affordable.
* This keyboard features standard split.
* Its very compact making it very portable
* It uses magnets to connect the splits allowing fast assembly.
* It uses Nice Nano V2(or Supermini nRF52840) with 5.4 bluetooth connectivity.



## Navigation

* [Assets](./Assets/)
* [Cad file](./Cad/)
* [Firmware](./Firmware/)
* [Production](./Production/)

### Variants

There is just one variant right now. 

`Cyprus HW` : Cyprus Handwired

## BOM 
*I have only included the component which is 'specific' to my cad design*

| Part  | price(INR) | price(USD) | link |
|-------|-----|-----------|------|
| Promicro NRF52840 | 758.00 |  7.98  | [link](https://robu.in/product/promicro-nrf52840-development-board/) |
| 3.7V LiPo Battery   | 139.00  | 1.46  | [link](https://robocraze.com/products/witty-fox-120mah-rechargeable-3-7v-lipo-battery?_pos=6&_sid=47fff7de1&_ss=) |
| Slide Switch | 9 | 0.095 | [link](https://robocraze.com/products/slide-switch-3-pin-2-way-spdt?_pos=1&_sid=5bdbba5e9&_ss=r) |


## Firmware

*Note: Before you understand firmware, you need to have a basic understanding of [how keyboard matrix work](https://docs.qmk.fm/how_a_matrix_works).*

This project uses [ZMK firmware](https://zmk.dev/docs) to code the board. Visit the link to read the documentation for a lot more information.

I am going to explain basics that you need to understand in the firmware. 

You assign board in file named `build.yaml`

``` 
include: 
  - board: nice_nano_v2
    shield: Cyprus_left
  - board: nice_nano_v2
    shield: Cyprus_right 
  - board: nice_nano_v2
    shield: settings_reset

```
You assign the common rows of the split in `<keyboard_name>.dtsi` file.

```    kscan0: kscan {
        compatible = "zmk,kscan-gpio-matrix";
        wakeup-source;
        diode-direction = "col2row";
        row-gpios = <&pro_micro 4 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>,
                    <&pro_micro 8 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>;
    };

```

You assign column in separate .overlay files

``` &kscan0 {
    col-gpios = <&pro_micro 21 GPIO_ACTIVE_HIGH>,
                <&pro_micro 14 GPIO_ACTIVE_HIGH>;
};

```

**Keymap**

 visit https://zmk.dev/docs/keymaps/behaviors

Standard keymap -

``` 
keymap {
        compatible = "zmk,keymap";

        default_layer {
            // -----------------------------------------------------------------------------------------
            // | `   |  1  |  2  |  3  |  4  |  5  |  6  |   |  7  |  8  |  9  |  0  |  -  |  =  | BKSP |
            // | TAB |  Q  |  W  |  E  |  R  |  T  |  Y  |   |  U  |  I  |  O  |  P  |  [  |  ]  |  \   |
            // | CAPS|  A  |  S  |  D  |  F  |  G  |  H  |   |  J  |  K  |  L  |  ;  |  '  | ENT |
            // | SHFT|  Z  |  X  |  C  |  V  |  B  |       |  N  |  M  |  ,  |  .  |  /  | SHFT|
            // | CTRL| GUI | ALT | SPC |             |       | SPC | MO1 | ALT | GUI | CTRL|
            // -----------------------------------------------------------------------------------------
            bindings = <
              &kp GRAVE &kp N1 &kp N2 &kp N3 &kp N4 &kp N5 &kp N6   &kp N7 &kp N8 &kp N9 &kp N0 &kp MINUS &kp EQUAL &kp BSPC
              &kp TAB   &kp Q  &kp W  &kp E  &kp R  &kp T  &kp Y    &kp U  &kp I  &kp O  &kp P  &kp LBKT  &kp RBKT  &kp BSLH
              &kp CLCK  &kp A  &kp S  &kp D  &kp F  &kp G  &kp H    &kp J  &kp K  &kp L  &kp SEMI &kp SQT          &kp RET
              &kp LSHFT &kp Z  &kp X  &kp C  &kp V  &kp B           &kp N  &kp M  &kp COMMA &kp DOT &kp FSLH       &kp RSHFT
              &kp LCTRL &kp LGUI &kp LALT &kp SPACE                 &kp SPACE &mo 1 &kp RALT &kp RGUI &kp RCTRL
            >;
        }; };

```

### Build and Configuration

#### Prerequisites

 *  Basic Soldering skill
 *  Access to 3d Printer
 *  A hot glue gun.

#### Cad 
*⚠️Important: I have not printed it myself so I do not gauranty that cad design would also work for you especially if you are choosing some commponent different than mine. That said, you would have to experiment with the cad design yourself.*

Print the [stl files](./Production/) using a 3d printer.

#### Wiring 

  First you need to wire everything up just like this schematics here. 

  ![alt](./Assets/Cyprus_Schematic.svg)

  Since I have not build it myself, I cant really show you the irl wiring photo. But if you want to know how to wire these effectively, I recommend you to watch any youtube video related to making handwire keyboard.

#### Compile and Flash

Now, you could follow the official method by zmk if you want to add your own personal touch to the firmware of your keyboard.

If you just want to use the pre-compiled firmware:

1. Connect the MCU of your **Left** half to your computer via USB.
2. Enter bootloader mode (usually by double-tapping the reset button). A new USB mass storage drive (e.g., `NICENANO`) should appear on your computer.
3. Copy the compiled left half `.uf2` file into this drive. The drive will automatically disconnect once the flashing is complete.
4. Repeat the same process for the **Right** half with the right half `.uf2` file.

### Poster

<img src="Assets\Edit_Gallery\Edit14.png">

<img src = "Assets\Edit_Gallery\Edit12.png">

-------------

### Contacts 

If you find any error or just want to help me improve or wanna work together — 

Drop the messege on my email: **itsmohammadsarfaraz@gmail.com**

If you like my work, follow me on instagram and drop a dm — [@ayysappling](https://www.instagram.com/ayysappling/)

----------

<div align = "center" > Made with love 💛 by Mohammad Sarfaraz </div>





