source /etc/keystone/admin-openrc.sh
#### 创建用户
openstack user create --password <> --email <> --domain <> name
#### 创建项目
openstack project create --domain <> --description <> <priject-name>
#### 创建角色
opensack <user> create <name>
#### 用户绑定角色
openstack role add--user <user> --project <project> <role>
#### 查询用户
openstack user list
openstack user show alice
#### 查询项目列表
openstack project list
#### 查询项目详细内容
openstack project show <>
#### 角色列表查询
openstack role list
#### 查询角色详细信息
openstack role show <>
#### 查询端点
openstack endpoint list
#### 创建镜像
glance image-create --name "" --ds-format qcow2 --container-format bare --progress < <image name>
#### 镜像列表
glance image-list
#### 镜像详细
glance image-show <ID>
#### 删除镜像
glance image-delete <ID>
#### 
