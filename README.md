# Performant Labs Jenkins agents

Build and push an image (e.g. php-agent):
```shell
cd php-agent
docker build -t php-agent .
docker tag php-agent:latest php-agent:8.2
docker tag php-agent:8.2 harbor.performantlabs.com/performantlabs/php-agent:8.2
docker push harbor.performantlabs.com/performantlabs/php-agent:8.2
```

Run agent on the server:
```shell
#public key from jenkins
export "PUB=ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCuWmHV10sm+9Du1bdBC88Y8sG+Xpe23zOU8Ud2cU232HyBv/5khfCO2+JxvTRkarSbN08HxVasHyS0meQRl5EVwNTCUbqBt9lo6ICxBAlCgnjSv8G4QZmWKJRftxlIt8tLPItcaGb+XD9VsK/46E7M6peC9OUD1d1LrZixRt2TUJGy6mqBHV3fDqcq46dJ6XPY6m+Xn13M5umZhClPY3NUeB4uAp2HXeKhq61DLR/aIVz6Bfdt2Irbpxir9ok75SMpL4qOHvGkly3aV7O75H/81tkNEWAAX3VTxZVuPc74fR1D9157ttAJLJFlyhedCOTFcAF9JUvXyWb1Q6sXL6GD7UEs8XRRBDYTkbdDa21hbY9UONLZoxFuQDGovpcfZThjqTFLcwgQsQ6EhwG43kuvPRH+z4nwqWGApcH8PxAEB0Cd0+8iOEPK71MG4GzgwNS/dA7mov/5Pl4LiHVKwOBl6exfd719zpd/MSOOxDrI2smDSXVArfcHPXX3rTTct4eIvCbLi6JNv+sWBcmfNKNZ5dSj/qyH31YDkwik8FMllWDRTf3pXZ7hWaxPTuWpmm/t8bn0zV7b9jR7bRFOr2sDubjFCCivpYEmpXAIP7AcIRAjGzJeVc0I1xDSFf7nqOY7Kvi/jYb43wnmvnB6XUc0IoXkhVsT1HjNzEGLQVZHMw== jenkins@7b02e3ce1f4c"
#choose a unique name
docker run -d --rm --name=agent-pooh -e "JENKINS_AGENT_SSH_PUBKEY=$PUB" --network=nginx_nginx harbor.performantlabs.com/performantlabs/php-agent:8.2
#test connect from jenkins to agent-pooh
docker exec  -it jenkins bash
#inside the container
ssh agent-pooh
```

Then 
 - go to [Manage Jenkins > Nodes](https://jenkins.performantlabs.com/manage/computer/new),
 - create a new agent,
 - clone, for example, 'agent1',
 - change host name
 - put appropriate labels.
