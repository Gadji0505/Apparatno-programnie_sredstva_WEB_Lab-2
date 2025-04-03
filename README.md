

// Коллекция болезней
db.Bolezn.insertMany([
 { _id: ObjectId(), name: "Грипп", type: "Вирусная инфекция", severity: "Средняя", contagious: true },
 { _id: ObjectId(), name: "Пневмония", type: "Бактериальная инфекция", severity: "Высокая", contagious: false },
 { _id: ObjectId(), name: "Гипертония", type: "Сердечно-сосудистое заболевание", severity: "Средняя", contagious: false },
 { _id: ObjectId(), name: "Диабет", type: "Обменное заболевание", severity: "Высокая", contagious: false },
 { _id: ObjectId(), name: "Астма", type: "Респираторное заболевание", severity: "Средняя", contagious: false },
 { _id: ObjectId(), name: "Аллергия", type: "Иммунологическое заболевание", severity: "Низкая", contagious: false },
 { _id: ObjectId(), name: "Гастрит", type: "Заболевание ЖКТ", severity: "Средняя", contagious: false }
])
 
// Коллекция симптомов
db.Symtom.insertMany([
 { _id: ObjectId(), name: "Кашель", type: "Респираторный", severity: "Средняя" },
 { _id: ObjectId(), name: "Лихорадка", type: "Инфекционный", severity: "Высокая" },
 { _id: ObjectId(), name: "Головная боль", type: "Неврологический", severity: "Низкая" },
 { _id: ObjectId(), name: "Боль в горле", type: "Респираторный", severity: "Средняя" },
 { _id: ObjectId(), name: "Насморк", type: "Респираторный", severity: "Низкая" },
 { _id: ObjectId(), name: "Высокое давление", type: "Кардиологический", severity: "Высокая" },
 { _id: ObjectId(), name: "Тошнота", type: "Гастроэнтерологический", severity: "Средняя" }
])
 
 
// Коллекция врачей
db.Doctor.insertMany([
 { _id: ObjectId(), name: "Иванов Иван", specialty: "Терапевт", experience: 10 },
 { _id: ObjectId(), name: "Петрова Анна", specialty: "Кардиолог", experience: 5 },
 { _id: ObjectId(), name: "Сидоров Петр", specialty: "Пульмонолог", experience: 15 },
 { _id: ObjectId(), name: "Козлова Мария", specialty: "Аллерголог", experience: 8 },
 { _id: ObjectId(), name: "Смирнов Дмитрий", specialty: "Гастроэнтеролог", experience: 12 },
 { _id: ObjectId(), name: "Кузнецова Елена", specialty: "Инфекционист", experience: 7 },
 { _id: ObjectId(), name: "Федорова Ольга", specialty: "Эндокринолог", experience: 10 }
])
 
// Коллекция назначений - упрощенная без внешних ключей
db.Naznachenie.insertMany([
 {  _id: ObjectId(), medication: "Парацетамол", dosage: "2 таблетки 3 раза в день" },
 {  _id: ObjectId(), medication: "Каптоприл", dosage: "1 таблетка 2 раза в день" },
 {  _id: ObjectId(), medication: "Амоксициллин", dosage: "500 мг 3 раза в день" },
 {  _id: ObjectId(), medication: "Супрастин", dosage: "1 таблетка 3 раза в день" },
 {  _id: ObjectId(), medication: "Омепразол", dosage: "20 мг 1 раз в день" },
 {  _id: ObjectId(), medication: "Оселтамивир", dosage: "75 мг 2 раза в день" },
 {  _id: ObjectId(), medication: "Инсулин", dosage: "По назначению врача" }
])
 
// Коллекция людей - упрощенная без внешних ключей
db.Pazhient.insertMany([
 {  _id: ObjectId(), name: "Петр Петров", age: 30},
 {  _id: ObjectId(), name: "Мария Иванова", age: 45},
 {  _id: ObjectId(), name: "Иван Сидоров", age: 25},
 {  _id: ObjectId(), name: "Анна Кузнецова", age: 50},
 {  _id: ObjectId(), name: "Дмитрий Смирнов", age: 35},
 {  _id: ObjectId(), name: "Елена Федорова", age: 60},
 { _id: ObjectId(), name: "Ольга Козлова", age: 28}
]);
// Получаем идентификаторы симптомов
const coughId = db.Symtom.findOne({ name: "Кашель" })._id;
const feverId = db.Symtom.findOne({ name: "Лихорадка" })._id;
const headacheId = db.Symtom.findOne({ name: "Головная боль" })._id;
const soreThroatId = db.Symtom.findOne({ name: "Боль в горле" })._id;
const runnyNoseId = db.Symtom.findOne({ name: "Насморк" })._id;
const highPressureId = db.Symtom.findOne({ name: "Высокое давление" })._id;
const nauseaId = db.Symtom.findOne({ name: "Тошнота" })._id;
 
// Получаем идентификаторы назначений
const paracetamolId = db.Naznachenie.findOne({ medication: "Парацетамол" })._id;
const captoprilId = db.Naznachenie.findOne({ medication: "Каптоприл" })._id;
const amoxicillinId = db.Naznachenie.findOne({ medication: "Амоксициллин" })._id;
const suprastinId = db.Naznachenie.findOne({ medication: "Супрастин" })._id;
const omeprazoleId = db.Naznachenie.findOne({ medication: "Омепразол" })._id;
const oseltamivirId = db.Naznachenie.findOne({ medication: "Оселтамивир" })._id;
const insulinId = db.Naznachenie.findOne({ medication: "Инсулин" })._id;
 
// Получаем идентификаторы болезней
const fluId = db.Bolezn.findOne({ name: "Грипп" })._id;
const pneumoniaId = db.Bolezn.findOne({ name: "Пневмония" })._id;
const hypertensionId = db.Bolezn.findOne({ name: "Гипертония" })._id;
const diabetesId = db.Bolezn.findOne({ name: "Диабет" })._id;
const asthmaId = db.Bolezn.findOne({ name: "Астма" })._id;
const allergyId = db.Bolezn.findOne({ name: "Аллергия" })._id;
const gastritisId = db.Bolezn.findOne({ name: "Гастрит" })._id;
 
// Получаем идентификаторы врачей
const therapistId = db.Doctor.findOne({ name: "Иванов Иван" })._id;
const cardiologistId = db.Doctor.findOne({ name: "Петрова Анна" })._id;
const pulmonologistId = db.Doctor.findOne({ name: "Сидоров Петр" })._id;
const allergistId = db.Doctor.findOne({ name: "Козлова Мария" })._id;
const gastroenterologistId = db.Doctor.findOne({ name: "Смирнов Дмитрий" })._id;
const infectiousBoleznId = db.Doctor.findOne({ name: "Кузнецова Елена" })._id;
const endocrinologistId = db.Doctor.findOne({ name: "Федорова Ольга" })._id;
 
// Получаем идентификаторы людей
const petrId = db.Pazhient.findOne({ name: "Петр Петров" })._id;
const mariaId = db.Pazhient.findOne({ name: "Мария Иванова" })._id;
const ivanId = db.Pazhient.findOne({ name: "Иван Сидоров" })._id;
const annaId = db.Pazhient.findOne({ name: "Анна Кузнецова" })._id;
const dmitryId = db.Pazhient.findOne({ name: "Дмитрий Смирнов" })._id;
const elenaId = db.Pazhient.findOne({ name: "Елена Федорова" })._id;
const olgaId = db.Pazhient.findOne({ name: "Ольга Козлова" })._id;
 
// Обновляем коллекцию Bolezn (добавляем симптомы и назначения)
db.Bolezn.updateMany(
   {},
   [
       { $set: {
           Symtoms: {
               $switch: {
                   branches: [
                       { case: { $eq: ["$name", "Грипп"] }, then: [coughId, feverId, soreThroatId, runnyNoseId] },
                       { case: { $eq: ["$name", "Пневмония"] }, then: [coughId, feverId] },
                       { case: { $eq: ["$name", "Гипертония"] }, then: [highPressureId, headacheId] },
                       { case: { $eq: ["$name", "Диабет"] }, then: [] },
                       { case: { $eq: ["$name", "Астма"] }, then: [coughId] },
                       { case: { $eq: ["$name", "Аллергия"] }, then: [runnyNoseId] },
                       { case: { $eq: ["$name", "Гастрит"] }, then: [nauseaId] }
                   ],
                   default: []
               }
           },
           prescriptions: {
               $switch: {
                   branches: [
                       { case: { $eq: ["$name", "Грипп"] }, then: [paracetamolId, oseltamivirId] },
                       { case: { $eq: ["$name", "Пневмония"] }, then: [amoxicillinId] },
                       { case: { $eq: ["$name", "Гипертония"] }, then: [captoprilId] },
                       { case: { $eq: ["$name", "Диабет"] }, then: [insulinId] },
                       { case: { $eq: ["$name", "Астма"] }, then: [] },
                       { case: { $eq: ["$name", "Аллергия"] }, then: [suprastinId] },
                       { case: { $eq: ["$name", "Гастрит"] }, then: [omeprazoleId] }
                   ],
                   default: []
               }
           }
       }}
   ]
);
 
// Обновляем коллекцию Pazhient (добавляем болезни и врача)
db.Pazhient.updateMany(
   {},
   [
       { $set: {
           Bolezns: {
               $switch: {
                   branches: [
                       { case: { $eq: ["$name", "Петр Петров"] }, then: [fluId] },
                       { case: { $eq: ["$name", "Мария Иванова"] }, then: [hypertensionId] },
                       { case: { $eq: ["$name", "Иван Сидоров"] }, then: [pneumoniaId] },
                       { case: { $eq: ["$name", "Анна Кузнецова"] }, then: [diabetesId] },
                       { case: { $eq: ["$name", "Дмитрий Смирнов"] }, then: [asthmaId] },
                       { case: { $eq: ["$name", "Елена Федорова"] }, then: [gastritisId] },
                       { case: { $eq: ["$name", "Ольга Козлова"] }, then: [allergyId] }
                   ],
                   default: []
               }
           },
           Doctor: {
               $switch: {
                   branches: [
                       { case: { $eq: ["$name", "Петр Петров"] }, then: infectiousBoleznId },
                       { case: { $eq: ["$name", "Мария Иванова"] }, then: cardiologistId },
                       { case: { $eq: ["$name", "Иван Сидоров"] }, then: pulmonologistId },
                       { case: { $eq: ["$name", "Анна Кузнецова"] }, then: endocrinologistId },
                       { case: { $eq: ["$name", "Дмитрий Смирнов"] }, then: pulmonologistId },
                       { case: { $eq: ["$name", "Елена Федорова"] }, then: gastroenterologistId },
                       { case: { $eq: ["$name", "Ольга Козлова"] }, then: allergistId }
                   ],
                   default: null
               }
           }
       }}
   ]
);
 
// Обновляем коллекцию Naznachenie (добавляем связь с человеком)
db.Naznachenie.updateMany(
   {},
   [
       { $set: {
           person: {
               $switch: {
                   branches: [
                       { case: { $eq: ["$medication", "Парацетамол"] }, then: petrId },
                       { case: { $eq: ["$medication", "Каптоприл"] }, then: mariaId },
                       { case: { $eq: ["$medication", "Амоксициллин"] }, then: ivanId },
                       { case: { $eq: ["$medication", "Инсулин"] }, then: annaId },
                       { case: { $eq: ["$medication", "Супрастин"] }, then: olgaId },
                       { case: { $eq: ["$medication", "Омепразол"] }, then: elenaId },
                       { case: { $eq: ["$medication", "Оселтамивир"] }, then: petrId }
                   ],
                   default: null
               }
           }
       }}
   ]
);
 
// Проверка результата
print("Связи успешно созданы. Пример данных:");
 
// Проверка коллекции Bolezn
print("Коллекция Bolezn:");
db.Bolezn.find().forEach(doc => {
   print(`Болезнь: ${doc.name}, Симптомы: ${doc.Symtoms}, Назначения: ${doc.prescriptions}`);
});
 
// Проверка коллекции Pazhient
print("\nКоллекция Pazhient:");
db.Pazhient.find().forEach(doc => {
   print(`Пациент: ${doc.name}, Болезни: ${doc.Bolezns}, Врач: ${doc.Doctor}`);
});
 
// Проверка коллекции Naznachenie
print("\nКоллекция Naznachenie:");
db.Naznachenie.find().forEach(doc => {
   print(`Лекарство: ${doc.medication}, Пациент: ${doc.person}`);
});













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






1. Топ 2 заболеваний по распространенности
2. Найти пациентов старше 30 лет с указанными заболеваниями (отсортировать по возрасту, вывести первых 2)
3. Количество врачей в возрастных группах по специальности
4. Количество рецептов по специальностям врачей
1)db.Pazhient.aggregate([
  { $unwind: "$diseases" }, // Разворачиваем массив болезней
  { 
    $group: { 
      _id: "$diseases", 
      count: { $sum: 1 } 
    } 
  },
  { 
    $lookup: { 
      from: "Bolezn", 
      localField: "_id", 
      foreignField: "_id", 
      as: "bolezn_info" 
    } 
  },
  { $unwind: "$bolezn_info" },
  { 
    $project: { 
      name: "$bolezn_info.name", 
      count: 1, 
      _id: 0 
    } 
  },
  { $sort: { count: -1 } },
  { $limit: 2 }
])
2)db.Pazhient.aggregate([
  { 
    $match: { 
      age: { $gt: 30 },
      diseases: { 
        $in: [
          db.Bolezn.findOne({ name: "Гипертония" })._id,
          db.Bolezn.findOne({ name: "Диабет" })._id
        ] 
      } 
    } 
  },
  { 
    $lookup: { 
      from: "Bolezn", 
      localField: "diseases", 
      foreignField: "_id", 
      as: "bolezn_data" 
    } 
  },
  { $sort: { age: 1 } },
  { $limit: 2 },
  { 
    $project: { 
      name: 1, 
      age: 1, 
      diseases: "$bolezn_data.name" 
    } 
  }
])
3)db.Doctor.aggregate([
  { 
    $match: { 
      specialty: "Терапевт" 
    } 
  },
  { 
    $bucket: {
      groupBy: "$experience",
      boundaries: [0, 5, 10, 15, 20],
      default: "Other",
      output: { 
        count: { $sum: 1 } 
      }
    } 
  }
])
4)db.Naznachenie.aggregate([
  { 
    $lookup: { 
      from: "Pazhient", 
      localField: "person", 
      foreignField: "_id", 
      as: "pazhient" 
    } 
  },
  { $unwind: "$pazhient" },
  { 
    $lookup: { 
      from: "Doctor", 
      localField: "pazhient.doctor", 
      foreignField: "_id", 
      as: "doctor" 
    } 
  },
  { $unwind: "$doctor" },
  { 
    $match: { 
      "doctor.specialty": { 
        $in: ["Терапевт", "Кардиолог"] 
      } 
    } 
  },
  { 
    $group: { 
      _id: "$doctor.specialty", 
      total_prescriptions: { $sum: 1 } 
    } 
  }
])
