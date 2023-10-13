# CAVE Related Repo Overview

Services
- [NeuroglancerJSONServer](https://github.com/seung-lab/NeuroglancerJsonServer)
- [PyChunkedGraph](https://github.com/seung-lab/pychunkedgraph/)
- [EMAnnotationSchemas](https://github.com/seung-lab/emannotationschemas/)
- [AnnotationEngine](https://github.com/seung-lab/annotationengine/)
- [MaterializationEngine](https://github.com/seung-lab/materializationengine/)
- [Level2Cache](https://github.com/seung-lab/PCGL2cache)
- [AnnotationFrameworkInfoService](https://github.com/seung-lab/AnnotationFrameworkInfoService)
- [Authentication](https://github.com/seung-lab/neuroglancer-auth)
  
Deployment
- [Deployment](https://github.com/seung-lab/CAVEDeployment)
- [Deployment Instructions](https://docs.google.com/document/d/1C110QZEWdE4NnAIR7HLStKhff3d4Ha60VJ_W09akj3c/edit)

Service Libraries
- [DynamicAnnotationDB](https://github.com/seung-lab/dynamicannotationdb/) For MaterializationEngine and AnnotationEngine
- [Authentication Client](https://github.com/seung-lab/middle_auth_client) For all services

Client Libraries
- [CAVEClient](https://github.com/seung-lab/CAVEClient) Service API access
- [MeshParty](https://github.com/sdorkenw/MeshParty) Mesh download and processing
- [PCG_skel](https://github.com/AllenInstitute/pcg_skel) skeletonization
- [NeuroglancerAnnotationUI](https://github.com/seung-lab/NeuroglancerAnnotationUI) pandas>neuroglancer pipeline

Viewer/Front End
- [Neuroglancer](https://github.com/seung-lab/neuroglancer/)
- [dash-on-flask](https://github.com/fcollman/dash-on-flask/) Generic dash serving flask service
- [flywire-dash-apps](https://github.com/seung-lab/FlyWireDashApps.git) Dash apps for flywire
- [connectivity-viewer](https://github.com/ceesem/dash-connectivity-viewer) Dash apps for generic data

Misc Libraries
- [MultiWrapper](https://github.com/sdorkenw/MultiWrapper)


[system_overview]: https://github.com/seung-lab/AnnotationPipelineOverview/blob/master/systemoverview.png "System Overview"

The system is designed to accept 'annotations' of volumetrically segmented EM data, and facilitate producing an up-to-date 'materialized' view of those annotations that reflect the current state of segmentation (as stored in the PyChunkedGraph).  The system is built to be maximally agnostic to the type of annotations that are stored in the system, and all annotation definitions are kept in EMAnnotationSchemas, which is the source of truth about what types of annotations can exist.  The DynamicAnnotationDB simply stores these data with appropriate lookups of what supervoxel_ids have which annotations, and vice-versa. The MaterializationEngine serves to merge data from the PyChunkedGraph and DynamicAnnotationDB and insert data into a database, presently implemented as a PostGIS database, interfaced through SqlAlchemy models, which are dynamically defined in EMAnnotationSchemas.  The AnalysisDataLink library will faciliate user interactions with the materialized database to assist in making common queries. 
