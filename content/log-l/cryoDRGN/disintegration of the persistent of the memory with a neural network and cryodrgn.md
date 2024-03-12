Using cryoDRGN to process a dataset to see if we can make the reconstruction any better.
Draco dormiens nunquam tiltillandus.

- First, train nn on low resolution images using the default architecture as an initial pass to sanity check results and remove junk particles, 
- After any particle filtering, then larger models can potentially learn more heterogeneity
- After validation, etc, train on the full resolution images.

Initial motivation: well, let's see if cryoDRGN works on the dataset and see the latent spaces
check whether clusters that amounts to anything;

cryoDrgn doesn't really overfit, if we do binning, the streaks wouldn't occur. Why tho? we don't really know yet.

How to filter out the bad particles?
latent space maps particules to volumes
select volumes from the latent space,
visually inspect the volumnes and filter out bad ones and map out the particle stack.

How do we know what's good vs what's bad for a cluster/particle stack?
- Avik: we know this by visually looking at the volumes, look for the helico linkers
- we didn't know where the streaks come from but we just decided to come 
