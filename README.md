# AnnotationPipelineOverview

- [Neuroglancer](https://github.com/seung-lab/neuroglancer/)
- [NeuroglancerAnnotationUI](https://github.com/seung-lab/NeuroglancerAnnotationUI)
- [NeuroglancerJSONServer](https://github.com/seung-lab/NeuroglancerJsonServer)
- [PyChunkedGraph](https://github.com/seung-lab/pychunkedgraph/)
- [EMAnnotationSchemas](https://github.com/seung-lab/emannotationschemas/)
- [AnnotationEngine](https://github.com/seung-lab/annotationengine/)
- [AnnotationFrameworkClient](https://github.com/seung-lab/AnnotationFrameworkClient)
- [DynamicAnnotationDB](https://github.com/seung-lab/dynamicannotationdb/)
- [MaterializationEngine](https://github.com/seung-lab/materializationengine/)
- [AnalysisDataLink](https://github.com/seung-lab/analysisdatalink/)
- [AnnotationFrameworkInfoService](https://github.com/seung-lab/AnnotationFrameworkInfoService)
- [Deployment](https://github.com/seung-lab/AnnotationFrameworkDeployment)
- [Authentication](https://github.com/seung-lab/neuroglancer-auth)
- [MeshParty](https://github.com/sdorkenw/MeshParty)
- [MultiWrapper](https://github.com/sdorkenw/MultiWrapper)

![alt text][system_overview]

[system_overview]: https://github.com/seung-lab/AnnotationPipelineOverview/blob/master/systemoverview.png "System Overview"

The system is designed to accept 'annotations' of volumetrically segmented EM data, and facilitate producing an up-to-date 'materialized' view of those annotations that reflect the current state of segmentation (as stored in the PyChunkedGraph).  The system is built to be maximally agnostic to the type of annotations that are stored in the system, and all annotation definitions are kept in EMAnnotationSchemas, which is the source of truth about what types of annotations can exist.  The DynamicAnnotationDB simply stores these data with appropriate lookups of what supervoxel_ids have which annotations, and vice-versa. The MaterializationEngine serves to merge data from the PyChunkedGraph and DynamicAnnotationDB and insert data into a database, presently implemented as a PostGIS database, interfaced through SqlAlchemy models, which are dynamically defined in EMAnnotationSchemas.  The AnalysisDataLink library will faciliate user interactions with the materialized database to assist in making common queries. 

[system deployment]
Presently, our deployment of this system is done on Google Cloud with considerable use of Google Kubernetes Engine.  The PyChunkedGraph and DynamicAnnotationDB, both make use of Google BigTable as their backend.  We are using CloudSql to host the postgres databases that back the AnnotationFrameworkInfoService and the 'materialized' backend interface.  We use Google DataStore to back the NeuroglancerJsonServer.  We are preparing a release of the scripts, manifest yaml files and setup instructions we have developed for spinning up our present deployment.  Each of the services could be in principle be deployed independantly, as they are in general only loosely coupled.  
