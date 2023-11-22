# ��������� � ������ � Git � GitHub
Git - ������� �������� ������

--

## ����������� �� GitHub
1.

## �������� ���������� �����������
1. ����� � ������� GitHub
	>https://github.com/username
	
2. ������� �����������
	- Repositories
	- New 
	- ������ ��������
	- 	

## SSH-�����
1. ���������� SSH-����
	>$ ssh-keygen -t rsa -b 4096 -C "����������� �����, � ������� �������� ��� ������� �� GitHub"
	
2. ���������� ���������� ����� � ����� ������:
	>$ clip < ~/.ssh/id_rsa.pub
	
3. ����������� SSH-���� � GitHub
	> ������� � ������� GitHub -> Settings -> SSH and GPG keys -> New SSH key -> ������ �������� � ��������� ������������� � ����� ������ ���� -> Add SSH key
	
4. �������� �����
	>$ ssh -T git@github.com
	>
	>������ YES
	>
	>�������� � �����: *Hi %���_�������%! You've successfully authenticated, but GitHub does not provide shell access.*
	
--
	
