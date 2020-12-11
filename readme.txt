mongod --replSet cmpos --logpath "r1.log" --dbpath ./rs1 --port 27018 &
mongod --replSet cmpos --logpath “r2.log" --dbpath ./rs2 --port 27019 &
mongod --replSet cmpos --logpath “r3.log" --dbpath ./rs3 --port 27020 &


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
