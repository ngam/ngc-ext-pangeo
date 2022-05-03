Rewriting Pangeo Docker ML containers (https://github.com/pangeo-data/pangeo-docker-images) based on NGC containers.

---

The basic workflow:

1. Pull an image from NGC

2. Add related tools to said image (inside each folder):

    a. For TensorFlow, add jax and other libraries

    b. For PyTorch, add PyTorch-Lightning and other DGL

3. Add universal geo-specific deps (from the root of the repo)

---

Handling complex dependencies: (TBD)
