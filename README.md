1
db.peopleNew.find({}, { name: 1, age: 1, diseases: 1 }).sort({ age: -1 });
2
db.peopleNew.aggregate([
 { $unwind: "$diseases" },​
 { $group: { _id: "$diseases", count: { $sum: 1 } } }
]);
3
const fluId = db.disease.findOne({ name: "Грипп" })._id;
db.peopleNew.find({ diseases: fluId }, { name: 1, age: 1 }).sort({ age: 1 });
4
db.prescriptionNew.aggregate([
 { $group: { _id: "$medication", count: { $sum: 1 } } }
]);
5
db.doctor.aggregate([
 { $group: { _id: "$specialty", maxExperience: { $max: "$experience" } } }
]);
6
db.peopleNew.aggregate([
 { $unwind: "$diseases" },
 { $group: { _id: "$diseases", avgAge: { $avg: "$age" } } }
]);
7
db.peopleNew.aggregate([
 { $unwind: "$diseases" },
 { $group: { _id: "$diseases", count: { $sum: 1 } } },
 { $sort: { count: -1 } },
 { $limit: 1 }
]);
8
db.prescriptionNew.aggregate([
 { $group: { _id: "$doctor", diseaseCount: { $sum: 1 } } },
 { $match: { diseaseCount: { $gt: 2 } } },
 { $project: { _id: 0, specialty: "$_id" } }
]);
9
db.peopleNew.aggregate([
 {
   $match: {
     diseases: {
       $in: db.disease.aggregate([
         { $match: { severity: "Высокая" } },
         { $group: { _id: null, diseaseIds: { $push: "$_id" } } }
       ]).next().diseaseIds
     }
   }
 },
 {
   $project: { name: 1, _id: 0 }
 }
]);
10
db.doctor.find({
   _id: {
       $in: db.peopleNew.distinct("doctor", {
           diseases: {
               $in: db.disease.distinct("_id", { severity: "Высокая" })
           }
       })
   }
});11
db.prescriptionNew.find({}, { medication: 1, dosage: 1, person: 1 }).sort({ person: 1 });
﻿1 Вывести имена пациентов и названия болезней, которыми они болеют, отсортированные по возрасту пациентов в порядке убывания.
﻿﻿2 Вывести названия болезней и количество пациентов,
страдающих каждой болезнью.
﻿﻿3 Вывести имена и возраст всех пациентов с диагнозом "Грипп", отсортированных по возрасту.
﻿﻿4 Подсчитать количество назначений каждого лекарства.
﻿﻿5 Найти врачей с максимальным опытом работы в каждой специальности.
﻿﻿6 Найти средний возраст пациентов, страдающих каждой болезнью.
﻿﻿7 Найти болезни, которыми страдает больше всего людей.
﻿﻿8 Вывести специальности врачей, которые лечат более двух болезней (через назначения).
﻿﻿9 Найти пациентов, у которых есть хотя бы одна болезнь с тяжестью "Высокая".
10.
Найти всех врачей, которые выписывали лекарства для
болезней с тяжестью "Высокая".
11. Вывести имена пациентов и дозировку лекарств, которые им назначены, отсортированные по имени пациента.