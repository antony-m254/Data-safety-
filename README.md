import paramiko
import os

def fetch_sftp_files(sftp_host, username, password, remote_path, local_path):
    transport = paramiko.Transport((sftp_host, 22))
    transport.connect(username=username, password=password)
    sftp = paramiko.SFTPClient.from_transport(transport)
    files = sftp.listdir(remote_path)
    
    for file in files:
        sftp.get(os.path.join(remote_path, file), os.path.join(local_path, file))
        
    sftp.close()
    transport.close()
