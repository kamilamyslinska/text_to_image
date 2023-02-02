# text_to_image

This project is a code test #diffusion-models-class channel on the Hugging Face Discord server.

It show how to use Stable Diffusion to create and modify images using existing pipelines.

There are multiple different versions of Stable Diffusion, with the latest at the time of writing being version 2.1. If you'd like to explore an older version, simply replace the model ID with the appropriate model (for example, you could try "CompVis/stable-diffusion-v1-4" or pick a model from the dreambooth concepts library).

If you're running out of GPU memory, there are some things you can do to reduce the RAM usage:

Load the FP16 version (not supported on all systems). With this you may also need to convert tensors to torch.float16 when experimenting with individual components of the pipeline:

pipe = StableDiffusionPipeline.from_pretrained(model_id, revision="fp16", torch_dtype=torch.float16).to(device)

Enable attention slicing. This reduces GPU memory usage at the cost of a small reduction in speed:

pipe.enable_attention_slicing()

Reduce the size of the images you're generating

Key arguments to tweak:

Width and height specify the size of the generated image. They must be divisible by 8 for the VAE to work (which we'll see in a future section).
The number of steps influences the generation quality. The default (50) works well, but in some cases you can get away with as few as 20 steps which is handy for experimentation.
The negative prompt is used during the classifier-free guidance process, and can be a useful way to add additional control. You can leave it out, but many users find it useful to list some undesirable descriptions in the negative prompt as shown above.
The guidance_scale argument determines how strong the classifier-free guidance (CFG) is. Higher scales push the generated images to better match the prompt, but if the scale is too high the results can become over-saturated and unpleasant.
If you're looking for prompt inspiration, the Stable Diffusion Prompt Book is a good place to start.

This project show image about Łódź, city in Poland.
