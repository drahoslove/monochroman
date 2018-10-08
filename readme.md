# Monochroman

Web based generator of monochromatic images.
(demo: http://apps.yo2.cz/monochroman/)

## What is it for
It generates black & white (just two colors, not grayscale) images.

It can be used for monochromatis displays (e-paper / e-ink) which are capable of producing only 2 colors.

Also for artistic purposes.

## What it can do
Several types of dithering filters:
 - fixed treshold
 - ordered filters
    - simple cluttered/disparsed 3×3
    - Bayer 2x2, 4×4, 8×8
 - error diffustion filters
    - Floyd-Steinberg
    - Atkinson 
    - Jarvis-Judice-Ninke
    - Sierra 3
    - Stucky
  
Aditional features:
 - Add noise to prevent digital artifacts from occuring
 - Adjust brightness and contrast of intermediate grayscale image
 - Narrow range of depth in which error diffusion is applyed

## Examples
(zoom page 200% or 300% to better se the differences)

**raw**

| Fixed treshold     | cluttered 3×3      | Bayer 2×2          | Bayer 4×4          | Bayer 8×8          |
|--------------------|--------------------|--------------------|--------------------|--------------------|
| ![img](ex/0.-.png) | ![img](ex/0.0.png) | ![img](ex/0.1.png) | ![img](ex/0.2.png) | ![img](ex/0.3.png) |

| Floyd-Steinberg    | Atkinson           | Jarvis-Judice-Ninke | Sierra 3          | Stucky             |
|--------------------|--------------------|--------------------|--------------------|--------------------|
| ![img](ex/0.4.png) | ![img](ex/0.5.png) | ![img](ex/0.6.png) | ![img](ex/0.7.png) | ![img](ex/0.8.png) |

**with added noise and reduced range**

| Fixed treshold     | Bayer 2×2          | Floyd-Steinberg    | Stucky             |
|--------------------|--------------------|--------------------|--------------------|
| ![img](ex/1.-.png) | ![img](ex/1.1.png) | ![img](ex/1.4.png) | ![img](ex/1.8.png) |

**adjusted brightness and contrast**

|                    | On 2.9" waveshare e-paper display |
|--------------------|--------------------|
| ![img](ex/x.8.png) | <img src="ex/epd.jpg" width="360px" /> |


## I/O

- Can open files of common image formats (**png**, **jpeg** and whatewer si compatible with html5 canvas)
- Can save to **png** or co custom **bitmap** format.
- Can POST bitmap over http to somewhere.

### Bitmap format

Outputed bitmap format is very simple. First 4 bytes define width and height (Big endian), rest is bitmap itself - one bit per pixel.

Eg.: *(file with 8×8 chess pattern)* 

bin:
```
 00000000 00001000 > width
 00000000 00001000 > height
 01010101 10101010 \
 01010101 10101010  \ pixels 
 01010101 10101010  / 0=Black, 1=White
 01010101 10101010 / 
```
hex:
```
 00 08 00 08 AA 55 AA 55 AA 55 AA 55
```

### Backend connection
Edit `BACKEND_URL` constant on line 6 to enable pushing bitmap to your http server to which `send button` will be sending bitmap, where you can do whatewer you want with it

*TODO - commit example of own backend*

## UI
![img](ex/monochroman.png)

## Source of knowlge
  - http://www.efg2.com/Lab/Library/ImageProcessing/DHALF.TXT
