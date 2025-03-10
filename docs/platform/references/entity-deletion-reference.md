---
title: Entity deletion reference and Force Delete
description: This topic covers the rules governing the deletion of Harness entities, and the Enable Force Delete of Harness Resources setting
sidebar_position: 4
helpdocs_topic_id: amj1oz4x4k
helpdocs_category_id: fb16ljb8lu
helpdocs_is_private: false
helpdocs_is_published: true
---

This topic covers the rules governing the deletion of Harness entities, and how to override it with a forceful delete.

### Entity connections

Entities are connected. A Role entity is applied to User entities. Deleting an entity, such as a Role, impact Users.

As a result of the connection between entities, deleting an entity can make another entity not able to do its job.

Harness will warn you if you try to delete an entity that is used by another entity or resource.

If you try to delete the following entity types, Harness will warn you if the entity is used elsewhere:

* User groups
* Connectors
* Secrets
* Templates
* Services

If the entity is used, Harness will show you where.

For example:

* A Pipeline that uses a Connector.
* A Connector that uses a Secret.

Harness provides you with the option to delete the entity from all dependent entities (bulk removal).

### Permissions

The ability to delete an entity depends on the Role permissions you have. You can see the Delete permissions in any role:

![](./static/entity-deletion-reference-00.png)
In some cases, you might try to delete an entity, but the entity is used by another entity that you do not have permission to change.

Harness will identify that you do not have permission to edit the other entity, and so you cannot delete this entity.

### Role deletions

When attempting to delete a role, you will see all the Groups assigned to it.

Role Id has the following deletion rules:

* The role’s Id can't be used until it is completely removed from the database (based on the retention policy).
* If the deleted role effects active users, they are prevented from performing the operations granted by the removed role’s permissions.   
For example, if a user was assigned to a role that had the Create/Edit Pipeline permission, and the role is removed, then the user can no longer create or edit Pipelines.

### User deletions

A User entity is identified by their Id. The Id is the email address used to invite and sign up the User:

![](./static/entity-deletion-reference-01.png)

A User and its Id can be deleted. 

When a User is deleted, their Id (email address) can’t be used until the User is completely removed from the system. See [Entity Retention Policy](entity-retention-policy.md).

### Pipeline deletions

When you delete a Pipeline, Harness will list all the related entities that will be deleted from Harness.

Pipeline deletion has the following rules:

* All runtime entities (deployments) are deleted from the Harness and are not available in any reports.
* When there is a reference to a deleted deployment, such as in a report, there is an indication that the deployment is deleted.
* The Pipeline is removed from Harness and is not available.
* All [input sets and overlays](../pipelines/input-sets) in the deleted pipeline are deleted also.

### Project deletions

When you delete a Project, Harness will list all the related entities that will be deleted from Harness.

Project deletion has the following rules:

* All Project resources (Pipelines, Services, Environments, etc) are deleted.
* Project Delegates are deleted from Harness. You will have to remove the Harness Delegate(s) from your environment.
* All Project Users are notified via email that the Project was deleted.

## Enable Force Delete of Harness Resources

You can force delete a Harness entity even if your pipelines or other entities reference it. Following are the entities that you can force delete in Harness:
- Connectors
- Secrets
- Service
- Infrastructure
- Environments
- Environment Groups
- Templates
- File Store files

  
The Harness account admin can enable or disable the force delete option in the account's default settings.  It is generally recommended that this setting be turned on only for brief periods due to the interconnectivity nature of the Harness entities. 

![](../references/static/force-delete-new.png)

This topic explains the steps to force delete a connector.

1. In your Harness Account, go to your Project.
2. In Project Setup, click Connectors.
3. Click the three dots corresponding to the connector you want to delete.
4. Click Delete.
   For any connector that you try to delete, one of the following holds true:
   1. Connector is not referenced in any Harness entity - If your connector is not referenced in any Harness entity, you can delete it by clicking Delete.
   2. Connector is referenced in Harness entities - If your connector is referenced in a Pipeline or any other Harness entity, you can view the corresponding references or force delete it by selecting Forcefully delete this connector now.
      
      ![](../references/static/forcedelete2.png) 


You can view the details of all the Harness entities that you force delete in the Harness Audit logs.

When you force delete any Harness entity, the resources that reference it will be affected.

![](../references/static/forcedelete3.png)

As an example, if a template is being referenced and it is forcefully deleted, pipeline users will see this type of error message in their pipeline.  
![](../references/static/forcedelete-missingobj.png)


However, error messages and error results will vary depending on the entity deleted.  To avoid this, it is recommended to remove the entity from all the resources that reference it as a first step, and to only utilize Force Deletion as final step after all others have been exhausted.
### See also

* [Harness Entity Reference](harness-entity-reference.md)
* [Entity Retention Policy](entity-retention-policy.md)
* [Entity Identifier Reference](entity-identifier-reference.md)

