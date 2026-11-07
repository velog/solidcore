`SmPrimitiveCreation::CreateLinearSweep` makes each end cap with
`CreatePlanarFaceWith3DCurves` (the profile's outer loops grouped with the loops
directly inside them, each group one face in one construction) instead of
`CreatePlanarFacesWith3DCurves`, which starts from a face over the whole plane and
adds the loops one by one, each splitting a face and classifying against every
loop before it: the cap of a profile with n holes took n^2 (5041 holes: 27.6 s of a
60 s extrude). The faces, loops and vertices are the same (a plate with 1024 square
holes: 129 s and 0.09 s). Not in the C++ fork; a speed fix of our own.
