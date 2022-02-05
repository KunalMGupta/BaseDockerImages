# BaseDockerImages

Base Docker Images build on top of NVIDIA CUDA XX.X and includes anaconda, other useful packages. 

This repo now supports code-server also, so you get to enjoy all the cool features of VS code inside the docker! This was made possible primariy by scavenging the awesome repo https://github.com/works-on-my-machine/pytorch-code-server . So please check that out as well if you found this repo useful. 

Jupyter notebook is also supported now! So you can have the fun of working with pytorch with CUDA inside jupyter notebooks, all the while having access to a VS code interface! 

Note: The code-server project currently doesn't support downloading extensions from VS code market place due to some proprietary software issues. Instead, it relies on https://open-vsx.org/ for common extensions. Moreover, installing extensions is a bit painful at the moment, the only way you can do that is to do it from CLI as mentioned in this discussion: https://github.com/coder/code-server/issues/4333#issuecomment-941453418

