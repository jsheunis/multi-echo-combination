# Methods for combining multi-echo fMRI data

## Background

Multi-echo fMRI sequences acquire a slice or multiple slices of a functional image at discrete echo times (TE) after a single transverse excitation pulse of the scanner. All slices of a whole brain image are acquired within the standard repetition time (TR) which then yields multiple echoes per volume. The relaxation of the fMRI signal in a given voxel after transverse excitation, assuming a mono-exponential decay model, is given as:

$
\mathrm{S}\left(t\right)= \mathrm{S0} \cdot e^{
\frac{-t}{\mathrm{T2^{\ast}}}} + \varepsilon = \mathrm{S0} \cdot e^{-t \cdot 
\mathrm{R2^{\ast}}} + \varepsilon
$

with $S(t)$ being the time-decaying fMRI signal, S0 being the tissue magnetisation directly after transverse excitation, and $T2*$ being the local tissue transverse relaxation (i.e. decay time) constant (the inverse of the decay rate, $R2*$). Per-voxel estimates of $S0$ and $T2*$ can be derived using a log-linear regression estimation and the available echo times ($t_1$ to $t_{\mathrm{N}}$, where $pinv$ is the pseudo-inverse log the natural logarithm):

$
\left[\begin{array}{c}\log \left(\mathrm{S0}\right) \\ \mathrm{R2^{*}}\end{array}\right] = pinv\left(\left[\begin{array}{l}
1-t_{1} \\
1-t_{2} \\
\space\space\space\space\vdots \\
1-t_{\mathrm{N}}
\end{array}\right]\right) *
\left[\begin{array}{l}
\log \left(\mathrm{S}\left(t_{1}\right)\right) \\
\log \left(\mathrm{S}\left(t_{2}\right)\right) \\
\space\space\space\space\space\space\space\space\space\vdots \\
\log \left(\mathrm{S}\left(t_{\mathrm{N}}\right)\right)
\end{array}\right]
$

The mathematics of all widely used multi-echo combination schemes are based on the underlying concepts of data weighting, summation and averaging. Importantly, the multi-echo combination schemes presented here use the convention of weighted summation with normalised weights. This implies that (1) all weights are normalised such that their sum equals 1, then (2) each normalised weight is multiplied by its corresponding data point, then (3) these products are summed to produce the weighted summation.

## Simple echo summation

Simple echo summation assumes equal weights for all echoes (totalling $N$), which is calculated for an individual echo $n$ as:

$
    w_{n}^{\mathrm{SUM}}=\mathrm{\frac{1}{N}}
$

## tSNR-weighted combination

The PAID method put forward by Poser et. al (2006) uses the voxel-based tSNR measured at each echo ($\mathrm{tSNR}_{n}$) as the weights:

$
w_{n}^{\mathrm{tSNR}}=\frac{\mathrm{tSNR}_{n} \cdot \mathrm{TE}_{n}}{\sum_{i=1}^{\mathrm{N}} \mathrm{tSNR}_{i} \cdot \mathrm{TE}_{i}}
$

## TE-weighted combination

Purely using each echo's echo time, $TEn$, as the weight for that echo has also been suggested (Posse, 1999). In this case, the same scalar value is used as the weighting factor for all voxels of a specific echo:

$
w_{n}^{\mathrm{TE}}=\frac{\mathrm{TE}_{n}}{\sum_{i=1}^{\mathrm{N}} \mathrm{TE}_{i}}
$

Similarly, a range of scalar values can be used as echo-dependent weighting factors, usually optimised according to study-specific criteria. For example, Marxen et al (2016) selected scalar weights in order to yield an average $T2*$ value of 30 ms in their region of interest (the amygdala). In such a case, the predefined scalar weights {$\mathrm{SW_1}$, $\mathrm{SW_2}$, . . ., $\mathrm{SW_N}$} can be normalised as: 

$
w_{n}^{\mathrm{SW}}=\frac{\mathrm{SW}_{n}}{\sum_{i=1}^{\mathrm{N}} \mathrm{SW}_{i}}
$

## T2*-weighted combination

The T2*-weighted combination scheme used by Posse (1999) and termed "optimal combination" by Kundu et al (2012), calculates the individual echo weights $w_n$ per voxel as:

$
w_{n}^{\mathrm{T2^{\ast}}}=\frac{\mathrm{TE}_{n} \cdot \exp \left(-\mathrm{TE}_{n} / \mathrm{T2^{*}}\right)}{\sum_{i=1}^{\mathrm{N}} \mathrm{TE}_{i} \cdot \exp \left(-\mathrm{TE}_{i} / \mathrm{T2^{*}}\right)}
$

## T2*FIT-weighted combination

Finally, real-time $T2*$-mapping is made possible when using multi-echo fMRI. Here, the per-volume estimation of $T2*$ at each voxel, termed $T2*FIT(t)$, can also be used as the weighting factor in a per-volume echo combination scheme:

$
w_{n}^{\mathrm{T2^{\ast}FIT}}(t)=\frac{\mathrm{TE}_{n} \cdot \exp \left(-\mathrm{TE}_{n} / \mathrm{T2^{*}FIT}(t)\right)}{\sum_{i=1}^{\mathrm{N}} \mathrm{TE}_{i} \cdot \exp \left(-\mathrm{TE}_{i} / \mathrm{T2^{*}FIT}(t)\right)}
$

The per-volume nature of this echo combination scheme makes it ideal for use in both offline and real-time applications, when an a priori $T2*$-map is not available or not preferred.