# schemaless-aggregat
 export const find = (name, query, hint = {}, sort = {}, limit = 0,filter={},skip=0) => {
    return new Promise((resolve, reject) => {
      mongoose.connection.db.collection(name, (err, res) => {
        if (err) reject(err);
        // .explain("executionStats")
        resolve(
          res
            .find({ $query: query, $hint: { ...hint } },{...filter})
            .sort(sort)
            .skip(skip)
            .limit(limit)     
            .toArray()
            
        );
       
      });
    });
  };

export const findWithAggregation = (name, aggregate) => {
  return new Promise((resolve, reject) => {
    mongoose.connection.db.collection(name, (err, res) => {
      if (err) reject(err);
      // .explain("executionStats")
      resolve(
        res
          .aggregate([...aggregate]).toArray()

      );

    });
  });
};
