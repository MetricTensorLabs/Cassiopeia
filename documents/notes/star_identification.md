# Star Identification

## Mortari (et al.) - The Pyramid Star Identification Technique (2004)

ABSTRACT: A new highly robust algorithm, called Pyramid, is presented to identify the stars observed by star trackers in the general lost-in-space case, where no a priori estimate of pointing is available. At the heart of the method is the k-vector approach for accessing the star catalog, which provides a searchless means to obtain all cataloged stars from the whole sky that could possibly correspond to a particular measured pair, given the measured interstar angle and the measurement precision. The Pyramid logic is built on the identification of a four-star polygon structure — the Pyramid — which is associated with an almost certain star identification. Consequently, the Pyramid algorithm is capable of identifying and discarding even a high number of spikes (false stars). The method, which has already been tested in space, is demonstrated to be highly efficient, extremely robust, and fast. All of these features are supported by simulations and by a few ground test experimental results.


<p align="center">
  <img src="https://github.com/MetricTensorLabs/Star-Tracker/blob/main/documents/notes/figs/pyramid_flowchart.png" width="700">
  </br>
  <em>Fig. Pyramid algorithm flowchart</em>
</p>

## Brady (et al.) - The Inertial Stellar Compass: A New Direction in Spacecraft Attitude Determination (2002)

Star identification can be accomplished in many different ways and is a widely accepted method for attitude determination onboard many types of spacecraft. The ISC software uses Mortari’s Pyramid algorithm. This algorithm presents a fast and robust star identification technique applicable to WFOV cameras that does not use a searching phase. The Pyramid algorithm is capable of identifying stars without any prior attitude knowledge in less than 1 minute on the ISC target processor running at 4 MHz. Furthermore, the algorithm is extremely tolerant of spikes. For the ISC application, four valid centroids will provide a false match frequency of only 5x10e-5. The ISC software uses Mortari’s ESOQ-2 algorithm to determine a star-camera quaternion from the identified stars.

The Mortari Pyramid algorithm was further modified to use prior attitude knowledge provided by the gyros. Specifically, the K-vector method has been modified to trim the number of candidate star pairs that would normally be returned, according to the direction of the camera boresight. This filtering is especially important given the sizeable centroid errors, and hence the large sample of candidate star pairs associated with a WFOV design.

## Samuel (et al.) - Design and Performance of an Open-Source Star Tracker Algorithm on Commercial Off-The-Shelf Cameras and Computers (2020)

We pass the measured bearing vectors to a triangle star search algorithm that processes sets of three stars at each iteration of a loop. To avoid reusing false positive stars repeatedly for numerous successive iterations, we employ an algorithm to search through the catalog with as few repeated stars as possible; this algorithm reduces the number of successive cycles without reuse of recent stars. Our algorithm is a modification of a reflector identification (REFLID) algorithm, which itself is a modification of the Pyramid star ID approach.

## Smith - Development and implementation of star tracker based attitude determination (2017)

An accurate and fast star identification technique is the core of what makes a star tracker unique. What most methods boil down to is a pattern matching algorithm. The traditional method involves matching angles between stars in an image with the angles between those stored in the star catalog. Mortari has developed a few different star identification schemes. One method Mortari provides is the pyramid star identification technique that takes four stars in an image and compares the resulting pyramid with his catalog. An alternative is to leverage the spherical area and polar moment of inertia of a spherical triangle formed by a star triad in an image. The method was quickly expanded to the planar triangle, and although the authors made no direct comparison between the two methods, their results show better performance from the planar case. The method of star identification presented here follows closely to that provided by Houtz and Frueh, who expand on the triangle properties. Their star identification is based on comparing four different properties in order to provide higher accuracy. By comparing five planar triangle properties, the aim of this work is to decrease false star identification and provide a robust process that connects the star identification process with the custom star catalog formation.

## Tennenbaum - Automatic Star-Tracker Optimization Framework (2017)

Current state of the art, fast star-tracker algorithms can trace their origins back to the work of Dr. Daniele Mortari from Texas A&M, who developed the Pyramid Star Identification Technique for Lost in Space star identification[1]. Lost in Space refers to the situation where there is no prior knowledge of satellite orientation. In essence, the pyramid technique works as follows:

1. The positions of stars in the image are determined by the centroiding technique. This is detailed in the image preprocessor section.

2. Possible four star constellations are generated, and checked to match a reference constellation database 

a. A pilot star is selected from an image 
b. Three reference stars are selected from the image 
c. The distance between the pilot star and the three reference stars are looked up in a “K-vector” database (a variant of the hash-table devised by Dr. Mortari and commonly used in the spacecraft guidance community) 
d. If a constellation has been uniquely identified, solve for spacecraft orientation, and identify the remaining stars by looking them up in a star database based on their position in the sky. Otherwise select the next constellation in the image 
e. Repeat until identification has occurred, or all combinations have been exhausted.

In the original paper, this technique was tested with a 12 degree field of view, and a database consisting of stars of magnitude greater than 5.5 magnitude. The algorithm is fine in this case, however the constellation database size quickly balloons and starts producing false positives when dimmer stars are included. It is necessary to include dimmer stars in order to ensure complete sky coverage with lower field of view sizes. Lower Field of view sizes are desirable due to the fact that they are the cheapest way to lower the number of degrees per pixel, which improves the accuracy of the final position estimate.

This issue was addressed by Dr. Mortari’s student Benjamin Spratling in his PHD thesis, describing a new startracker algorithm called Star-ND. In it, he proposes a new technique which involves selecting the three stars that are nearest to the pilot star, and simply using those as the basis for the star triangle. This allows each pilot star to have a single, unique constellation, which drastically reduces database size (cases where the nearest three stars might be ambiguous are handled by checking both cases). Finally, rather than performing three separate lookups and cross checking the results, it is possible to drastically increase performance by using a hash function which takes the angles between the star furthest from the pilot star and the two middle stars, and produces a number which is unique to each constellation. The end result is that it is possible to increase both accuracy and performance. This was tested in flight with an 8x8 fov camera, and a star tracker database consisting of 7.5 magnitude stars. However, it is assumed that centroiding accuracy is on the order of within 1/20 of a pixel of the database position, which requires that the camera be intentionally defocused in order to spread the light around among multiple pixels, as well as a very accurate database

In order to meet our goals, we need another order of magnitude Field of View improvement above Star-ND, while simultaneously reducing the accuracy requirement. This is accomplished by the following refinements to the algorithm

1. Rather than using the method for generating the database lookup key described in Star-ND, we order the stars by brightness, and use the brightest star as the pilot. We then simply measure the distance between pilot and the 2nd, 3rd and fourth brightest stars respectively, and use those values to form a key for the k- vector lookup. Cases where the relative brightness is ambiguous is handled similarly to the distance ambiguity, by inserting it into the database both ways. 

2. Memory usage is dramatically reduced by memory mapping the constellation database. This is a programming technique which intelligently loads bits and pieces of a file into memory as needed rather than reading the entire thing into memory.

For a case where average constellation width is 500 pixels, this results in a 1000x improvement in the maximum number of constellations which can quickly be looked up (resolving the ambiguity of the ordering of the values results in a 2x improvement, and adding a third value results in a 500x improvement).

This can also be traded for a 10x improvement in the amount of tolerable star position error.

## Smith - Development and Implementation of Star Tracker Based Attitude Determination (2017)

*This paper contains good literature review*</br>

Since the 1970’s, several star identification algorithms were created to answer the Lost in Space problem, and are separated into two categories of identification analysis: 
1. an instance of subgraph isomorphism, or 
2. pattern recognition. Subgraph isomorphism deals with the angular separations between the stars and their adjacent neighbors; pattern recognition associates stars with a pre-defined image pattern, such as is used in facial recognition.

The latter includes Grid algorithms, Neural networks, and Genetic algorithms. The focus of this study will be on the first classification of star identification methods using subgraph isomorphisms. Brief descriptions of several of the algorithms developed under this classification are presented below based on the author who created them. The terminologies used in this work are set in braces {} next to the authors’ original terminologies which are left intact to maintain the authors’ meaning.

<p align="center">
  <img src="https://github.com/MetricTensorLabs/Star-Tracker/blob/main/documents/notes/figs/bratt_star_identification_list.png" width="700">
  </br>
  <em>Fig. List of star identification methods and authors</em>
</p>

**J. Mortari**</br>
In 2004, Mortari et al. developed the Pyramid algorithm, supplemented with his k-vectoring technique. This algorithm uses a minimum of 4 stars for feature extraction and pattern creation. Mortari’s Pyramid design was described by Spratling as using an optimal permutation algorithm to exploit the ability of his algorithm to select which stars to match. This permutation is written to minimize the time spent considering stars that do not match, suspecting them to be non-star spikes (false spots) on the image plane. Mortari’s code had been tested to reject non-stars in an image containing only five real stars but with 63 non-stars included, however, this was done with very low centroiding error. He generated patterns beginning with the first star {spot} of the image being the apex of the pattern (one of the corners) and would select in turn the next two stars {spots} of the image to build a triad pattern. With this established, the next star {spot} in the image was selected to verify the validity of the triad. This 4th spot created another three possible triads, hence the impression of a Pyramid with 6 features. If this Pyramid did not match with the patterns in the sub-catalog {feature list}, then the algorithm kept the initial 3 stars {spots} and used the next observed star {spot} in the spot list to generate a new Pyramid.

<p align="center">
  <img src="https://github.com/MetricTensorLabs/Star-Tracker/blob/main/documents/notes/figs/pyramid.png" width="700">
  </br>
  <em>Fig. Basic star triangle and pyramid</em>
</p>

In above figure, the three vertices $(i, j, k)$ are the primary observable stars {spots} that the algorithm wishes to identify, and vertex $r$ is the fourth star {spot} used as verification, with $v$’s being the angular distance between the observable stars {spots}. With four triad patterns (each triad containing upwards of six features), the features are compared to patterns within the feature list using a feature tolerance. Out of a possible 24 features, Mortari uses only 6 for his identification. Furthermore, he uses a verification phase prior to returning a solution. 

The Pyramid algorithm was successfully tested in-flight on Draper’s “Inertial Stellar Compass” star tracker used on MIT’s satellites HETE and HETE-2. This algorithm is presently under exclusive contract to StarVision Technologies, thus, neither pseudo code, nor programming was obtainable due to infringement issues.

**Computational Considerations**
Mortari’s Pyramid algorithm was among the fastest in star identification computation. Using what Mortari called his “k-vector” approach, the amount of time required to search the database {catalog} and tables {feature lists} could be independent of the size of the database. This was the fastest among the algorithms in terms of database searching with equation $O(b)$ as the feature extraction and equation $O(k)$ as the database search, where $k$ is is the number of possible star {spot} pairs with inter-star angles within the tolerance and $b$ is the number of stars in the pattern.
