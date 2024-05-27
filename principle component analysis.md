[[principle component analysis]], also know as PCA, is a [[dimensionality reduction]] method applied in a variety of types of [[image mass spectrometry]] (IMS).

PCA subdivides the data in orthonormal principle components, which are linear combinations of the spectra found in IMS data. This means that principle components are pseudo spectra of the spectra in raw IMS data.

These pseudo spectra do not necessarily bear any biological significance, but are rather formed by concentrating as much data in one principle component as possible while maintaining their orthogonality. This way the most dominant patterns in the IMS data can be identified, and with further processing it can be deduced what the biological significance of these patterns is.

## Data Decomposition
The raw MSI data can be represented in $D \in \mathbb{R}^{p*b}$ , where $p$ forms a row per pixel, and each pixel gets $b$ columns, for each bin in the MSI spectra. **The matrix index is thus no indication of the pixel position the original image**.

The MSI data can be composed into the following; a loading matrix $L \in \mathbb{R}^{b*n}$ and a score matrix $S \in \mathbb{R}^{p*n}$.
$$ D = SL^\top $$
However, because [[singular value decomposition]]s have a computational advantage over eigenvalue decompositions, this is most commonly used
$$D = U\Sigma V^\top$$
Here $\Sigma$ is a diagonal matrix containing the singular values of $D$ in descending order. $U$ and $V$ contain the left- and right-singular vectors respectively.

Note that $D$ is rarely a square matrix. This means that its rank is always limited by the lesser of its rows and columns. This also limits the amount of non-zero singular values in $\Sigma$. Hence we know that $rank(\Sigma)=rank(D)\leq\min(p,b)$.

The loading matrix $L$ contains the eigenvectors of the covariance matrix $D^\top D$. Using the SVD we get 
$$\begin{aligned}
D^\top D &= (U\Sigma V^\top)^\top(U\Sigma V^\top)\\
&= V\Sigma^2 V^\top
\end{aligned}$$
So the right singular vectors in $V$ for an orthonormal basis for the mass spectral space. This is the mathematical meaning o f L. Hence, $L=V$, **if D is column centered**.

It must therefore be that $D = S*L^\top = U\Sigma L^\top$, meaning $S = U\Sigma$.

In simpler terms, a loading defines a pseudo spectrum, which explains a chunk of the raw data's variance. The scoring attributes a portion of a pseudo spectrum's gain to each pixel. **Note that generally speaking not all of the raw data variance is explained in the pseudo spectra**.

## Selecting Number of Components
The selection of the number of components can be done in 2 main ways.
## Preprocessing
- #### Autoscaling
	- each variable has its mean subtracted and is divided by its standard deviation. This yields that the PCS will be performed on the autocorrelation matrix, instead of covariance matrix. 
	- _may amp up noise_.
- #### Poisson scaling
	- **Uncorrelated does not mean statistically independent**
	- Because PCA is a variance based technique this works best on gaussian data. But Becasue the experiment counts collisions with a sensor both the noise and pure data will more likely follow a poission distribution.
	- In a Poisson distribution the mean and variance are identical. Hence, high peaks tend to have high noise. This can mess with the PCA decomposition
	- This negatively impacts the amount of PCs that will present as significant in the plots.
	- Poisson scaling intends to tackle this.
	- This maps the data to a different space before doing PCA.
		- $D^\text{new}_{i,:} = \frac{D_{i,:}}{mean(D_{i,:})}$
		- $D^\text{new}_{:,j} = \frac{D_{:,j}}{mean(D_{:,j})}$
- #### Filter Scaling
	- divide each peak by the standard deviation of pixels in the neighborhood. e.g. adjacent pixels.
	- This reduces local intensity variations and therefore also noise.
- #### Shift Variance Scaling
	- Based on same concept as Maximum Autocorrelation Factorisation (MAF)
	- Divide the peak by its standard deviation in the shift matrix
	- Shift matrix is obtained by a 1-pixel shifted D from the original D.
- #### Intensity Scaling with Priors
	- The raw IMS data is not an enigma. Professionals always have some insight in what compounds are to be expected in a specific diagnosis and where they are likely to occur. Therefore it is wise to careful diminish irrelevant peaks from the raw IMS data. In doing so the variance of irrelevant components is reduced and is therefore less likely to occur in the principal component analysis.

## Postprocessing
#### Varimax
In PCA decomposition there is rotational ambiguity. i.e. There is a infinite amount of orientations in which the data can be orthonormalised. This can be represented as
$$D = SL^\top = (SA)(R^{-1}B^T) = \tilde{A}\tilde{B}^\top$$
for any invertible transformation $R$.

The orientation with the highest variable in their first k components is not necessarily the most readable one. In order to increase the readability of the data $R$ is often used to rotate the PCA data in such a way that the resulting imagery is more readable. This does not impact the quality of the fit. However, if the scores are relaxed the individual components are then no longer uncorrelated.

#Varimax is a specific type of rotation that maximises the squared loadings while limiting itself to orthogonal rotations (Kaiser, 1958). This yields more sparsely filled loading vectors, which means increases contrast in the visualisation of the PCA data.

## Issues in PCA
#### Tissue Correlations
The state of the art PCA techniques currently treat each pixel as an independent sample. However, in reality the tissues that are being sampled can be spatially autocorrelated.

#### Data Size
Data can reach into the real of terabytes, far exceeding even undustrial RAM space. Therefore it is important for data to be preprocess though e.g. peak picking. However, this does come at the cost of the unsupervised nature of the analysis and is susceptible to human error in removal of relevant peaks.

Other ways are spectral and spatial binning, meaning smoothing the peaks by areaging over adjacent spectra or pixels respectively. This leads to loss of resolution in either domains and is not desirable.

