{% include mathjax.html %}



# Fourier Transformation

A Fourier series represents any periodic function as a sum of sine and cosine functions with appropriate coefficients. 
Since the sinusoids each have a representative frequency a periodic function in time can be analyzed in terms of its frequency. 
Time (t) and wavenumber (ω) are related by the fourier transform and have units of seconds and inverse seconds. 
We have already discussed changing basis sets in previous sections; however, we have not yet discussed how to transform between position and momentum. This is possible through what is commonly referred to as the *Fourier transformation*.

We can represent a state with either $\psi(x)$ or with $\phi(p)$ where 
Φ = momentum-space wavefunction, and Ψ = position-space wavefunction. 

With these variables, we are able to Fourier transform from one to the other using the following symmetric Fourier transform:

![Fourier](/fourier.png) 

(Note that this is only in 1-dimension) 

We are then able to use Euler's approximation $e^{ikx}=cos(kx)+isin(kx)$ show sinusoids as a wavenumber.

* Q: What can we expect to see when performing the Fourier transform between position and momentum?
* A: We can observe the following graphs generated in MatLab using this [code](/PosAndMomVarWidth.md).

![Four1](/four2.gif) 
![Four2](/four3.gif)

In each of the graphs represented, we have an observable particle in the position and momentum basis. The plane in the middle is at zero position (x = 0), and zero momentum (k = 0). We are able to observe that at a higher momemntum, there is a shortening in the wavelength, 
an increase in steepness, and an increase in energy. As time progresses, we see the evolution of both basis sets.

When the momentum is left shifted, the particle has momentum to the left. If the momentum increases, we observe a kinkier helix in the position space. Conversely, as position increases we see the opposite for the momentum wavepacket. The wider the position wavepacket, the slower the momentum evolves over time. As we would expect, when the position is at a maxima, the momentum is at a minumim as it is least defined in that moment. The same is true for the opposite relationship. 

*All we are doing in performing the fourier transformation is taking a function of x as a linear combination of sinusoidal functions or complex exponents and expressing them as a change of bases.* 



[Home](/README.md) 
