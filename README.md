#查询用户test1可以查看的页面
![](https://github.com/xujianhui1995/mis4/blob/master/1.png)
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
![](https://github.com/xujianhui1995/mis4/blob/master/2.png)
	 
#对订单(order)页面中的操作权限(sys_button)
![](https://github.com/xujianhui1995/mis4/blob/master/3.png)

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
![](https://github.com/xujianhui1995/mis4/blob/master/4.png)
 
