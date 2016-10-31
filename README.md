#查询用户test1可以查看的页面
	开始
	↓
输入用户名称test1、查询user表
	↓
UserID=4、查询userrole表
	↓
    RoleID=6
	↓PrivilegeMasterKey=6、PrivilegeAccess=Sys_Menu  查询cf_privilege表
   PrivilegeID
   	↓
    MenuName

##SQL语句：
	SELECT MenuName,MenuUrl 
	FROM sys_menu 
	where MenuID in
	(SELECT PrivilegeAccessKey 
	FROM cf_privilege 
	where PrivilegeMasterKey in
		(SELECT RoleID 
		FROM cf_role 
		where RoleID in
			(SELECT RoleID 
			FROM cf_userrole 
			where UserID in
				(SELECT UserID 
				FROM cf_user 
				where LoginName='test1')))
 	and PrivilegeAccess='Sys_Menu');
##查询结果：
	 
#对订单(order)页面中的操作权限(sys_button)
	开始
	↓
输入用户名称test1、查询user表
	↓
UserID=4、查询userrole表
	↓
    RoleID=6
    	↓PrivilegeMasterKey=6、PrivilegeAccess=Sys_Menu  查询cf_privilege表
   PrivilegeID
	↓
     MenuName
     	↓
   MenuName=订单、查询结果集
	↓
MenuNo= OrderManageOrders、查询button表
	↓
     按钮权限


SQL语句：
	SELECT * FROM sys_button
	where MenuNo=
	(select MenuNo from(
		SELECT * 
		FROM sys_menu 
		where MenuID in
			(SELECT PrivilegeAccessKey 
			FROM cf_privilege 
			where PrivilegeMasterKey in
				(SELECT RoleID 
				FROM cf_role 
				where RoleID in
					(SELECT RoleID 
					FROM cf_userrole 
					where UserID in
						(SELECT UserID 
						FROM cf_user 
						where LoginName='test1')))
		 			and PrivilegeAccess='Sys_Menu')) temp
	 where MenuName='订单');

##查询结果：
 
