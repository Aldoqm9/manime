# Cómo aprender Manim por cuenta propia.
Este tutorial funciona con la versión de [manim del 3 de Febrero del 2019](https://github.com/3b1b/manim/tree/3b088b12843b7a4459fe71eba96b70edafb7aa78). 
## 1. Modificar los siguientes archivos:
En ```manimlib/mobject/coordinate_systems.py``` agregar en la linea 54.

```python3
    def get_axis(self, min_val, max_val, axis_config):
        new_config = merge_config([
            axis_config,
            {"x_min": min_val, "x_max": max_val},
            self.number_line_config,
        ])
        return NumberLine(**new_config)
```
<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/capturas/coord_syst.png" width="700" /></p>

## 2. Modificar búsqueda de imágenes:
### 2.1 Descarga las siguientes imágenes
#### Imagen genérica .png a ```media/designs/raster_images```

<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/archivos/generic.png" width="400" /></p>

#### Imagen genérica .svg a ```media/designs/svg_images```

<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/archivos/generic.svg" width="400" /></p>

#### Después mueve los tres archivos .svg de ```manimlib/files``` a ```media/designs/svg_images```

### 2.2 Añade la siguiente linea en ```manimlib/mobject/svg/svg_mobject.py```

```python3
            os.path.join(SVG_IMAGE_DIR, "generic.svg")
```

<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/capturas/capt2.png" width="700" /></p>

### 2.3 Abre ```manimlib/mobject/types/image_mobject.py``` y remplaza la parte seleccionada de la imagen izquierda por el código que está en la parte derecha.


<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/capturas/capt3.png"/></p>

Código:
```python3
            path=self.select_image(filename_or_array)
            #path = get_full_raster_image_path(filename_or_array)
            image = Image.open(path).convert(self.image_mode)
            self.pixel_array = np.array(image)
        else:
            self.pixel_array = np.array(filename_or_array)
        self.change_to_rgba_array()
        if self.invert:
            self.pixel_array[:, :, :3] = 255 - self.pixel_array[:, :, :3]
        AbstractImageMobject.__init__(self, **kwargs)

    def select_image(self,file_name):
        extensions=[".jpg", ".png", ".gif"]
        possible_paths = [file_name]
        possible_paths += [
            os.path.join(RASTER_IMAGE_DIR, file_name + extension)
            for extension in ["", *extensions]
        ]
        possible_paths+=[os.path.join(RASTER_IMAGE_DIR, "generic.png")]
        for path in possible_paths:
            if os.path.exists(path):
                return path
```

### 2.4 Abre ```manimlib/for_3b1b_videos/pi_creature.py``` y remplaza la parte seleccionada de la imagen izquierda por el código que está en la parte derecha.

<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/capturas/capt4.png"/></p>

Código:
```python3
                "PiCreatures_plain.svg"
```

### 2.5 Abre ```manimlib/mobject/svg/drawings.py``` y remplaza las partes seleccionadas de la imagen izquierda por el código que está en la parte derecha.

<p align="center"><img src ="/Español/extras/aprender_manim_cuenta_propia_v1/capturas/capt5.png"/></p>

Códigos:
```python3
        "file_name": "Bubbles_speech.svg",
```
------------------------------------
```python3
            SVGMobject.__init__(self,file_name="Bubbles_speech" ,**kwargs)
```
