# restpack-resource [![Build Status](https://travis-ci.org/RESTpack/restpack-resource.png)](https://travis-ci.org/RESTpack/restpack-resource) [![Dependency Status](https://gemnasium.com/RESTpack/restpack-resource.png)](https://gemnasium.com/RESTpack/restpack-resource)

REST resource paging, side-loading, filtering and sorting:

```
class Group
  include DataMapper::Resource
  include RESTPack::Resource

  property :id, Serial
  property :name, String, :length => 128
  property :created_by, Integer, :required => true
  property :channel_id, Integer, :required => true
  timestamps :at

  validates_presence_of :name, :channel_id
  
  has n, :invitations
  has n, :memberships
  
  resource_can_include :memberships, :invitations
  resource_can_filter_by :channel_id, :created_by
  resource_can_sort_by :id
end
```