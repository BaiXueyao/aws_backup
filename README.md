# aws_backup
implement backup in the aws ec2 instance

For the ec2-back tool, I choose C and shell to finish it.

The tool is for NetBSD system, but I think it can work in most
of the Linux system.

When you execute `make` command, the executable ec2-back file
will appear. Then can use this file to run command like 
"./ec2-backup -r cat -l cat ${dir}"

Sometime the ec2-insatnce cannot log in that is because the
instance is not avaliable yet.
The time I set in this program is like below:
create_instance 	10s;
get_region 		1s;
get_avaliable_zone 	1s;
create_volume		20s;
attach_volume		2s;
execute_command		70s;
detach_volume		5s;
terminate_instance	0s.

If it does not work, maybe the instance is not good to access.
Please try again.

In this program, we handle some little tricky thing.
1. the private_key file, whether is has 400.
2. the path, we get the absolute path of the ${dir}.
3. the file descripter of STDOUT_FILENO, we use pipe() and 
   dup2() to handle this.

If you want to get the useful output information, you need to 
`export EC2_BACKUP_VERBOSE=*`, or `unset EC2_BACKUP_VERBOSE`.

