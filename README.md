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




Вот MongoDB-команды для выполнения поставленных задач:

---

### **1. Топ 2 заболеваний по распространенности**
```javascript
db.diseases.aggregate([
  { $group: { _id: "$name", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 2 }
])
```
*Предполагается коллекция `diseases` с полем `name` (название болезни).*

---

### **2. Найти пациентов старше 30 лет с указанными заболеваниями (отсортировать по возрасту, вывести первых 2)**
```javascript
db.patients.find({
  age: { $gt: 30 },
  diseases: { $in: ["Гипертония", "Диабет"] } // Пример заболеваний
}).sort({ age: 1 }).limit(2)
```
*Предполагается коллекция `patients` с полями `age` и `diseases` (массив заболеваний).*

---

### **3. Количество врачей в возрастных группах по специальности**
```javascript
db.doctors.aggregate([
  { 
    $match: { specialty: "Терапевт" } // Пример специальности
  },
  {
    $bucket: {
      groupBy: "$age",
      boundaries: [20, 30, 40, 50, 60], // Границы возрастных групп
      default: "Other",
      output: { count: { $sum: 1 } }
    }
  }
])
```
*Предполагается коллекция `doctors` с полями `age` и `specialty`.*

---

### **4. Количество рецептов по специальностям врачей**
```javascript
db.prescriptions.aggregate([
  {
    $lookup: {
      from: "doctors",
      localField: "doctor_id",
      foreignField: "_id",
      as: "doctor_info"
    }
  },
  { $unwind: "$doctor_info" },
  {
    $group: {
      _id: "$doctor_info.specialty",
      total_prescriptions: { $sum: 1 }
    }
  },
  { $match: { _id: { $in: ["Терапевт", "Хирург"] } } } // Пример специальностей
])
```
*Предполагается:*
- Коллекция `prescriptions` с полем `doctor_id`.
- Коллекция `doctors` с полями `_id` и `specialty`.

---

### Примечания:
1. Замените названия коллекций и полей на актуальные в вашей БД.
2. Для точного выполнения задач могут потребоваться дополнительные этапы агрегации или индексы.
