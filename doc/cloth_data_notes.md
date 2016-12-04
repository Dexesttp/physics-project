# Sturges : cloth data

## hclClothData (#108)

- Entry point
- Here : called "neck" for the googles around the neck.
- Links to all the relevant data :
  - SimClothData : data about how the cloth is simulated (constraints / collisions)
  - Buffer Definitions : defines engine-specific characteristics of the buffer
  - Transform set definitions : TODO
  - Operators : defines the operators  (TODO)
  - Cloth state data : Defines data bout the current state (engine stuff ?)
  - Actions : no idea (0 items)
  - Target platform : the platform to execute stuff on (`HCL_PLATFORM_x64`)

## hclSimClothData (#109)

- Simulation-related data
  - OverridableSimulationInfo : seems to be the global info about cloth stuff
    - Gravity : 4D vector (x/y/z/strength ?)
    - global damping by second : air resistance
    - Collision tolerance : deformation ? :o
    - Sub steps : probably the recursion level to calculate stuff (may hinder performance)
    - Pinch detection : no idea yet, but seems cool
    - Landscape collision : collision with land - might be a good idea to toggle on
    - Transfer motion : probably a thing to transfer the motion 'down' to other elements
  - name : the name of the item (useless for us)
  - particleDatas : define data about each particle
    - mass
    - inv (invariant ?) mass
    - radius
    - friction
  - fixedParticles : defines which particles are fixed and which are not
  - triangleIndices : defines the indices of the wanted triangles (related to the mesh ?)
  - triangle flips : no idea yet (5 * 0)
  - total mass : the total mass of the object
  - collidable transform map : collision with other parts of the mesh ? Contains a hclSimCLothDataCollidableTrandformMap
    - transformSetIndex
    - transformIndices
    - offsets
  - per instance collidables : references
  - static constraint sets : references to constraints applied on particles and such.
  - antiPinch constraint sets : no idea yet (there is 0)
  - simClothPoses : default state ? (one item)
  - actions : no idea still (still 0)
  - static collision masks : defines which particles are affected by static collision
  - per particle Pinch detection enabled flags : defines which particles are affected by pinch detection
  - collidable pincing data : list of pinch data ?
    - pinch detection enabled : enable/disbale pinch for this elements
    - pinch detection priority : the priority of this pinch related to others
    - pinch detection radius : the radius of effect of this pinch
  - Min pinched particle index : the first ID of the particle that can be pinched ?
  - Max pinched particle index : the last ID of the particle that can be pinched ?
  - max collision pairs : the maximum number of simultaneous collision handled
  - max paticle radius : the maximum radius a particle has (used for R-map resolution depth ?)
  - landscape collision data : contains a hclSimClothDataLandscapeCollisionData
    - landscape radius : the radius of elements of the landscape - seems to be the smallest possible int
    - enable stuck particle detection : detects if a particle is stuck int he landscape and free it (I guess)
    - stuck particle stretch factor SQ(uared ?) : the max allowed stretch befor the particle is freeed (if enabled)
    - pinch detection enabled : if landscape can cause pinch
    - Pinch detection priority : priority of a landscape pinch (related to other pinches ?)
    - pinch detection radius : the radius used for landscape pinch (why not hte first landscapeRadius then ?)
  - num landscape collidable particles : the number of particles that can collide with the landscape.
  - do normals : TODO (no idea, why is it true ?)
  - transfer motion data : I'm guessing what is used to configure how the motion is transfered down to toher elements

## hclCollidable (#110)

- Contains data about the collision object
  - name : useless
  - transform : the transform to apply to the shape
  - linear velocity : the velocity to apply tot hte shape (hair flow ? oO)
  - angular velocity : idem but for radii
  - pinch detection enabled : enables pinch detection for this collision box
  - Pinch detection priority : priority of the pinch detection event
  - Pinch detection radius : the radius needed to detect the pinch
  - Shape : reference to the actual collision shape

## hclTaperedCapsuleShape (#111)

- Contains the collidable shape, as a capsule
- Properties of the capsule (inferred, to check)
  - small : center of the low part of the cone
  - big : center of the big part of the cone
  - cone apex : the apex of the capsule's cone
  - cone axis : the axis of the capsule's cone
  - l vector / d vector : no idea yet (see cone ? capsules ?)
  - tan theta vector negative : for the engine I guess (from the values above)
  - small radius : the smallest radius to have a collision (from above)
  - big radius : the biggest radius to ahve a collision (from above)
  - l / d : no idea (probably related to the l/d vectors)
  - cos theta / sin theta / tan theta : from theta (for the engine)
  - tan theta squared : idem

## hclStandardLinkConstraintSet (#112)

- Contains all the normal links between particles
  - name : useless
  - links : the links
    - particle A : index of the first particle
    - particle B : index of the second particle
    - rest length : the length of the link at rest (meaning always because it's a standard constraint)
    - Stiffness : the stiffness of the link (not used ?)

## hclStretchLinkConstraintSet (#113)

- Contains all the non-standard links.
  - name : useless
  - links : the links
    - particle A : index of the first particle
    - particle B : index of the second particle
    - rest length : the length of the link at rest
    - Stiffness : the stiffness of the link (stretchness)

## hclLocalRangeConstraintSet (#114)

- Contains all the constraints based on particle-mesh interaction
  - name : useless
  - local constraints : list of the constraints
    - particle index : the index of the particle (-_-)
    - reference vertex : the vertex (of the mesh ?) to apply the constraint to.
    - maximum distance : the max distance between the particle and the vertex
    - max normal distance / min normal distance : no idea (inwards / outwards ?)
  - reference mesh buffer Idx (index ?) : the mesh buffer index
  - stiffness : the stiffness of the constraints i guess
  - shape type : SHAPE_SPHERE (shape of the constraints ? to use as "local constraints" types ?)
  - apply normal component : I guess it's a toggle between the "normal" and the "maximum distance" things above

## hclVolumeConstraintMx (#115)

- Contains all the constraints based on the total volume of the area I guess
- TODO

## hclBendStiffnessConstraintSet (#116)

- Contains all bend links between 4 particles
  - name : useless
  - links
    - weightA / weightB / weightC / weightD : the weight of the particle in the constraint
    - particleA / particleB / particleC / particleD : the ID of the particles
    - bend stiffness : the stifness of the link
    - rest curvature: the default (A, B, C, D) curve, I guess in degrees
  - Use rest pose config : no idea (true)

## hclSimClothPose (#117)

- The information about the default particle pose
  - name : useless
  - positions : position vectors by particle

## hclScratchBufferDefinition (#118)

- the information about the buffer to use (engine stuff ?)
  - name : useless
  - type : buffer type
  - subtype : buffer subtype
  - num vertices : the number of vertices this buffer can handle / contains
  - num triangles : idem but for tringles
  - buffer layout : the layout of the buffer
    - elements layout 1 / 4
      - vector conversion : no idea
      - vector size : no idea
      - slot ID : no idea
      - slot start : no idea
    - slots 1 / 4
      - flags : no idea
      - stride : no idea
    - num slots : actually not the above thing (maybe just the limit as they're hardcoded arrays)
    - triangle format : TF_OTHER (no idea)
  - triangle indices : no idea (0 elements)
  - store normals : should the buffer store normals ?
  - store tangents and bitangents : should the buffer ``

## hclBufferDefinition (#119)

- The information about another buffer to use
  - name : no idea
  - type : no idea
  - sub type : no idea
  - num vertices : the number of vertices this buffer can hold
  - num triangles : the number of triangles this buffer can hold
  - buffer layout : same thing as above

## hclTransformSetDefinition (#120)

- Define the transform set I guess ?
  - name : useless
  - type : no idea
  - num transforms : the number of total transforms (193)

## hclObjectSpaceSkinPNOperator (#121)

- No idea yet (TODO) - maybe skinnign stuff ?
  - name : useless
  - bone from skin mesh transforms : It may be a subset of the mesh skinning
  - transform subset : the related subset of transforms for the bone positions
  - output buffer index : no idea yet
  - transform set index : no idea yet
  - object space deformer : defines what bone deforms what
  - local PNs : locla positions of elements
  - local unpacked PNs : no idea (engine stuff ?)

## hclMoveParticlesOperator (#122)

- operator used to move particles
  - name : useless
  - vertex particles pairs : defines a pair of (vertex, particles) to move
    - vertex index
    - particle index
  - sim cloth index : the index of the cloth simulation (in the hclClothData ?)
  - ref buffer index : the index of the buffer (in the hclClothData ?)

## hclSimulateOperator (#123)

- simulation parameters
  - name : useless
  - sim cloth index : the index of the simulation cloth to apply (in the hclClothData ?)
  - sub steps : the number of substeps of this smulation operation to limit to (interesting but laggy to increase I guess)
  - number of solve iterations : same as above
  - constraint execution : order to execute the constraints (indexes in the hclClothData)
  - adapt constraint stiffness : wat ? (false)

## hclSimpleMeshBoneDeformOperator (#124)

- how to deform the mesh from bones
  - name : useless
  - input buffer index : the buffer to use as input
  - output transform set index : the output transform to apply to
  - triangle / bone pairs : explicit
    - bone offset
    - triangle offset
  - local bone transforms : matrices to transform the above bones by I guess

## hclGatherAllVerticesOperator (#125)

- The operator that retrieves all the good vertices form the mesh
  - name : useless
  - vertex input from vertex output : the IDs are weirdly defined
  - input buffer index : the input buffer to gather the vertices from
  - output buffer index : the buffer to put the retrieved vertices in
  - gather normals : also copy over the normals
  - partial gather : config option (copy all / copy part by part and keeps some outdated stuff ?)

## hclClothState (#125 and #126)

- defines a cloth state (simulated / not simulated ?)
  - name : useless
  - operators : operators to select from the `hclClothData` list.
  - used buffers : the buffers used while in this state
    - buffer index
    - buffer usage
      - per component flags (x4)
      - triangles read : true/false (read triangles in the buffer)
    - shadow buffer index : no idea
  - used transform sets :
    - transform set index
    - transform set usage
      - per component flags (x2)
      - per component transform trackers
        - read
          - storage
            - words
            - num bits
        - read before write
          - storage
            - words
            - num bits
        - written
          - storage
            - words
            - num bits
  - used sim cloths : indexes of the sim cloth data used.