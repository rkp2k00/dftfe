DFT-FE : Density Functional Theory With Finite-Elements 
=======================================================


About
-----

DFT-FE is a C++ code for materials modeling from first principles using Kohn-Sham density functional theory, developed by the [Computational Materials Physics Group](http://www-personal.umich.edu/~vikramg) at University of Michigan.
It is based on adaptive finite-element discretization that handles all-electron and pseudopotential calculations in the 
same framework, and incorporates scalable and efficient solvers for the solution of the Kohn-Sham equations. Importantly, DFT-FE can handle general geometries and boundary conditions, including periodic, semi-periodic and non-periodic systems. DFT-FE code builds on top of the deal.II library for everything 
that has to do with finite elements, geometries, meshes, etc., and, through deal.II on p4est for parallel adaptive mesh handling.

Directory structure of DFT-FE
-----------------------------
 - src/ (Folder containing all the source files of DFT-FE)
   - triangulation/
      - triangulationManager/
        - triangulationManager.cc (This class generates and stores adaptive finite element meshes for real-space DFT problem).
        - all other files part of triangulationManager.cc
      - meshMovement/
        - meshMovement.cc (Base class to move triangulation vertices)
        - meshMovementGaussian.cc (Class to move triangulation nodes using Gaussian functions attached to FE nodes)
        - meshMovementAffineTransform.cc (Class to update triangulation under affine transformation)
   - dft/
      - dft.cc (This class is the primary interface location of all other parts of the DFT-FE code for all steps involved in obtaining the Kohn-Sham DFT ground-state solution.)
      - vselfBinsManager.cc (Categorizes atoms into bins for efficient solution of nuclear electrostatic self-potential)
      - energyCalculator.cc (Calculates the ksdft problem total energy and its components)
      - all other files part of dft.cc
   - dftOperator/
      - operator.cc (abstract discrete FE operator base class)
      - kohnShamDFTOperatorClass.cc (Implementation class for building the Kohn-Sham DFT discrete operator and the action of the discrete operator on a single vector or multiple vectors)
      - all other files part of kohnShamDFTOperatorClass.cc
   - linAlg/
      - linearAlgebraOperations.cc (Contains linear algebra functions used in the implementation of an eigen solver)
      - linearAlgebraOperationsOpt.cc (part of linearAlgebraOperations.cc)
      - linearAlgebraOperationsInternal.cc (Contains internal functions used in linearAlgebraOperations)
      - pseudoGS.cc (part of linearAlgebraOperations.cc)
   - poisson/poissonSolverProblem.cc (poisson solver problem class)
   - force/
      - force.cc (class for computing configurational forces required for geometry optimization)
      - all other files part of force.cc
   - geoOpt/
      - geoOptIon.cc (problem class for atomic force relaxation solver)
      - getOptCell.cc (problem class for cell stress relaxation solver)
   - solvers/
      - cgSolvers/cgPRPNonLinearSolver.cc (Polak-Ribiere-Polyak Conjugate Gradient non-linear solver)
      - eigenSolvers/chebyshevOrthogonalizedSubspaceIterationSolver.cc (Chebyshev filtered orthogonalized subspace iteration solver)
      - dealiiLinearSolver.cc (class containing interface to dealii Linear solver infrastructure)
      - linearSolver.cc (abstract base class for linearSolver)
      - eigenSolver.cc (abstract base class for eigensolver)
      - nonlinearSolverProblem.cc (abstract base class nonlinear solver problem to be solved by the nonlinear solver)
      - nonLinearSolver.cc (abstract base class for nonlinear solver)  
   - symmetry/
      - symmetrizeRho.cc (class for density symmetrization based on irreducible Brillouin zone calculation)
      - initGroupSymmetry.cc (part of symmetrizeRho.cc)

 - utils/ (Folder containing commonly used utily functions in DFT-FE)
   - xmlTodftfeParser.cc (converts pseudopotential file from xml format to dftfe format)
   - pseudoConverter.cc (wrapper to convert pseudopotential file from upf to dftfe format)
   - constraintMatrixInfo.cc (Overloads functions associated with dealii's constraintMatrix class)
   - fileReaders.cc (Contains commonly used I/O file utils functions)
   - dftUtils.cc (Contains repeatedly used small functions in the KSDFT calculations)
   - dftParameters.cc (Infrastructure to parse input parameters from the input parameter file)
   - vectorTools/
     - vectorUtilities.cc (Contains generic utils functions related to custom partitioned flattened dealii vector)
     - interpolateFieldsFromPreviousMesh.cc (class to interpolate solutions fields from one finite element mesh to another) 

 - pseudoConvertors/upfToxml.cc (converts pseudopotential file from upf to xml format)



Installation instructions
-------------------------

The steps to install the necessary dependencies and DFT-FE itself are described
in the *Installation* section of the DFT-FE manual (doc/manual/manual.pdf). 


Running DFT-FE
--------------

Instructions on how to run DFT-FE including demo examples can be found in the *Running DFT-FE* section of the manual (doc/manual/manual.pdf). 


Contributing to DFT-FE
----------------------
Learn more about contributing to DFT-FE's development [here](https://github.com/dftfeDevelopers/dftfe/wiki/Contributing).


More information
----------------

 - See the official [website](https://sites.google.com/umich.edu/dftfe) for information on code capabilities, appropriate referencing of the code, acknowledgements, and news related to DFT-FE.
  
 - See Doxygen generated [documentation](https://dftfedevelopers.github.io/dftfe/).

 - For questions about DFT-FE, installation, bugs, etc., use the [DFT-FE discussion forum](https://groups.google.com/forum/#!forum/dftfe-user-group). 

 - For latest news, updates, and release announcements about DFT-FE please send an email to dft-fe.admin@umich.edu, and we will add you to our announcement mailing list.
 
 - DFT-FE is primarily based on the [deal.II library](http://www.dealii.org/). If you have particular questions about deal.II, use the [deal.II discussion forum](https://www.dealii.org/mail.html).
 
 - If you have specific questions about DFT-FE that are not suitable for the public and archived mailing lists, you can contact the following:
    - Phani Motamarri: phanim@umich.edu
    - Sambit Das: dsambit@umich.edu
    - Vikram Gavini: vikramg@umich.edu 

 - The following people have significantly contributed either in the past or current and advanced DFT-FE's goals: (All the underlying lists are in alphabetical order)
   - Principal developers  
       - Sambit Das (University of Michigan Ann Arbor, USA)
       - Dr. Phani Motamarri (University of Michigan Ann Arbor, USA)
    
   - Principal developers emeriti
       - Dr. Krishnendu Ghosh (University of Michigan Ann Arbor, USA)
       - Prof. Shiva Rudraraju  (University of Wisconsin Madison, USA)

   - Mentor
       - Prof. Vikram Gavini (University of Michigan Ann Arbor, USA)
         
 - A complete list of the many authors that have contributed to DFT-FE can be found at [authors](https://github.com/dftfeDevelopers/dftfe/blob/publicGithubDevelop/authors).    

License
-------

DFT-FE is published under [LGPL v2.1 or newer](https://github.com/dftfeDevelopers/dftfe/blob/publicGithubDevelop/LICENSE).
