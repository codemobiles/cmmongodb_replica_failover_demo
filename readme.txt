mkdir cm_replica_demo
cd demo
mkdir r1,r2,r3

mongod --replSet cmpos --logpath "r1.log" --dbpath ./r1 --port 27018 &
mongod --replSet cmpos --logpath “r2.log" --dbpath ./r2 --port 27019 &
mongod --replSet cmpos --logpath “r3.log" --dbpath ./r3 --port 27020 &


mongo --host cmpos/localhost:27018,localhost:27019,localhost:27020 

config = {_id: “cmpos”, members:[
 {_id: 0, host: “localhost:27018”},
 {_id: 1, host: “localhost:27019”},
 {_id: 2, host: “localhost:27020”}]
};

rs.initiate(config);
rs.status();

mongo --host yogi/localhost:27018,localhost:27019,localhost:27020
use courses
db.getCollection('test').find({})

#Doc
https://docs.mongodb.com/manual/replication/
https://studio3t.com/knowledge-base/articles/connect-to-mongodb/#connect-to-a-replica-set
www.codemobiles.com

ps -ef | grep mongod
