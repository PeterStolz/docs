.. _minio-mc-tag-set:

==============
``mc tag set``
==============

.. default-domain:: minio

.. contents:: Table of Contents
   :local:
   :depth: 2

.. mc:: mc tag set

.. |command| replace:: :mc:`mc tag set`
.. |rewind| replace:: :mc-cmd:`~mc tag set --rewind`
.. |versions| replace:: :mc-cmd:`~mc tag set --versions`
.. |versionid| replace:: :mc-cmd:`~mc tag set --version-id`
.. |alias| replace:: :mc-cmd:`~mc tag set ALIAS`

Syntax
------

.. start-mc-tag-set-desc

The :mc:`mc tag set` command sets one or more tags to a bucket or object.

.. end-mc-tag-set-desc

.. tab-set::

   .. tab-item:: EXAMPLE

      The following command sets tags for the ``mydata`` bucket on the
      ``myminio`` MinIO deployment:

      .. code-block:: shell
         :class: copyable

         mc tag set myminio/mydata "tag1=value1&tag2=value2"

   .. tab-item:: SYNTAX

      The command has the following syntax:

      .. code-block:: shell
         :class: copyable

         mc [GLOBALFLAGS] tag set                   \
                          [--rewind "string"]       \
                          [--versions]              \
                          [--version-id "string"]*  \
                          ALIAS                     \
                          "TAGS"

      .. include:: /includes/common-minio-mc.rst
         :start-after: start-minio-syntax
         :end-before: end-minio-syntax

      :mc-cmd:`mc tag set --version-id` is mutually exclusive with
      multiple parameters. See the reference documentation for more information.


Parameters
~~~~~~~~~~

.. mc-cmd:: ALIAS
   :required:

   The :ref:`alias <alias>` for a MinIO deployment and the
   full path to the object on which to apply the tag (e.g. bucket and path to
   object). For example:

   .. code-block:: none

      mc tag set myminio/mybucket/object.txt

.. mc-cmd:: TAGS
   :required:

   An ampersand-seperated (``&``) list of key-value pairs
   (``KEY=VALUE``), where each pair represents one tag to assign to the object.
   For example:

   .. code-block:: none

      mc tag set myminio/mybucket/object.txt "key1=value1&key2=value2"

.. mc-cmd:: --exclude-folders
   :optional:

   .. versionadded:: RELEASE.2024-01-11T05-49-32Z

   When used with :mc-cmd:`~mc tag set --recursive`, causes :mc:`mc tag set` to **not** traverse child prefixes.
   Tags are only applied to objects at the specified path.
   Requires :mc-cmd:`~mc tag set --recursive`.

   The following example applies the tag ``destination=international`` to objects at ``vacation-photos/cancun/`` but not ``vacation-photos/cancun/ocean/`` or other prefixes.
   
   For example, the above would add the tags to the object at``vacation-photos/cancun/pretty-beach.jpg`` but not to the object at``vacation-photos/cancun/ocean/tropical-fish.jpg``.

   .. code-block:: shell

      mc tag set myminio/vacation-photos/cancun "destination=international" --exclude-folders --recursive
   
.. mc-cmd:: --recursive, r
   :optional:

   .. versionadded:: RELEASE.2023-05-04T18-10-16Z

   Recursively applies the tag to all objects at the path specified to :mc:`ALIAS <mc tag set ALIAS>`.

.. mc-cmd:: --rewind
   :optional:

   .. include:: /includes/facts-versioning.rst
      :start-after: start-rewind-desc
      :end-before: end-rewind-desc

.. mc-cmd:: --versions
   :optional:   

   .. include:: /includes/facts-versioning.rst
      :start-after: start-versions-desc
      :end-before: end-versions-desc

   Use :mc-cmd:`~mc tag set --versions` and 
   :mc-cmd:`~mc tag set --rewind` together to apply the tag all object
   versions which existed at a specific point in time.

.. mc-cmd:: --version-id, --vid
   

   .. include:: /includes/facts-versioning.rst
      :start-after: start-version-id-desc
      :end-before: end-version-id-desc

   Mutually exclusive with the following parameters:

   - :mc-cmd:`~mc tag set --rewind`
   - :mc-cmd:`~mc tag set --versions`

Global Flags
~~~~~~~~~~~~

.. include:: /includes/common-minio-mc.rst
   :start-after: start-minio-mc-globals
   :end-before: end-minio-mc-globals

Examples
--------

Apply Tags to a Bucket or Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use :mc:`mc tag set` to apply tags to a bucket or object:

.. code-block:: shell
   :class: copyable

   mc tag set ALIAS/PATH "TAGS"

- Replace :mc-cmd:`ALIAS <mc tag set ALIAS>` with the 
  :ref:`alias <alias>` of the MinIO deployment.

- Replace :mc-cmd:`PATH <mc tag set ALIAS>` with the path to the bucket
  or object on the MinIO deployment.

- Replace :mc-cmd:`TAGS <mc tag set TAGS>` with one or more ampersand-separated
  (``&``) key-value pairs for each tag and its corresponding value.

Behavior
--------

S3 Compatibility
~~~~~~~~~~~~~~~~

.. include:: /includes/common-minio-mc.rst
   :start-after: start-minio-mc-s3-compatibility
   :end-before: end-minio-mc-s3-compatibility
