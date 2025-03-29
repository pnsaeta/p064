{:menu PR}


# Project Ideas

* toc
{:toc}

## Celestial Mechanics

### Janus and Epimetheus

Two moons of Saturn, Janus and Epimetheus, have almost identical orbits, which makes them seem to almost bounce off each other every four years or so. See [this NASA page](https://solarsystem.nasa.gov/moons/saturn-moons/epimetheus/in-depth/) for a description of this remarkable system.

### Kirkwood Gaps

The Titius-Bode formula,
\begin{equation}
  a_n = \frac{4 + 3 \times 2^{n-1}}{10}
\label{eq:titius-bode}
\end{equation}
predicts the positions of the planets in the solar system, as illustrated in Fig.&nbsp;1.

<p class="center" markdown="0">
  <img src="figs/PR-Bode.webp" style="width: 400px;" alt="">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1</a> — The red dots show the actual orbital radii of the planets; the blue curve shows the prediction of the Titius-Bode formula, Eq.&nbsp;(\ref{eq:titius-bode}).</p>

Until Neptune, the agreement with the Titius-Bode formula is remarkably good. However, there is a suspicious gap in the data: where is the missing planet between Mars and Jupiter? Indeed, that is where the asteroid belt lives. So, there is a bunch of material at roughly the radius predicted by the Titius-Bode formula, but the material never coalesced into a planet. Given Jupiter's size, it seems plausible that the giant planet played a role in preventing the debris from coalescing.

A closer look at the asteroid belt shows that there are gaps at certain radii, where no (or relatively fewer) asteroids are found. These are called **Kirkwood gaps**. They turn out to have orbital periods that, when divided by Jupiter's period, form ratios of small integers; e.g., 2/3, 3/5, etc. Simulate the motion of an asteroid in a circular orbit at a range of radii in the asteroid belt under the influence of the Sun and Jupiter. Can you find evidence of Kirkwood gaps?

### Proxima Centauri

The closest star to our solar system is the binary $$\alpha$$ Centauri,
with masses 1.10 and 0.85 solar masses, having an average
separation of *about* 23 A.U. (One astronomical unit is the mean
distance from the earth to the sun.) The system has a period of about
80 years with an eccentricity of 0.52. (The eccentricity $$\epsilon$$ of
an ellipse is given by $$\epsilon = c/a$$, where the distance from
the center to one focus is $$ c = \sqrt{a^{2}- b^{2}} $$, $$a$$ is
the semimajor axis, and $$b$$ is the semiminor axis.) 
For the purposes of this problem, ignore the *average* separation of the stars; take instead the period of their orbit 
to be *exactly* 80 years. You can then use Kepler's third 
law
\begin{equation}
	T^{2} = \frac{4\pi^{2} \mu}{k} a^{3}
	\label{eq:KeplerIII}
\end{equation}
to figure out the necessary orbital parameters. In this 
expression, $$\mu$$ is the reduced mass of the two stars (their 
product over their sum), and $$k = GM_{1}M_{2}$$.

Investigate the motion of a planet of about the size of the Earth
around such a system. To avoid large numbers, use a system of units in
which time is measured in years, and masses are measured in solar
masses. The most difficult part of this problem is finding suitable
initial conditions and a suitable reference frame in which to observe the planet's motion.
You may simplify
the problem somewhat by first solving for the motion of the two stars,
then assuming that their motion is not significantly affected by the
planet. I offer some guidance below, but recommend consulting a
mechanics text such as Marion, Goldstein, or Symon regarding the
motion of planets. You may also find Chapter 4 of Gould and Tobochnik
useful.

## Mechanics

### Metronomes

The basic idea is that we have multiple metronomes that all lie on the same platform. What we see in the following videos is that over time, all of the metronomes "synchronize." They all end up ticking at the exact same time, even though they all started at different points.
( https://www.youtube.com/watch?v=5v5eBf2KwF8&t=181s or https://www.youtube.com/watch?v=Ov3aeqjeih0 )