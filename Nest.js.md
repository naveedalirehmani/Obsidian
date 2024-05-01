
`npm g controller items`

to generate a controller called items.

1. **Decorator**
	1. **@body() createItemDTO : createItemType** : to populate the body of a incoming request on a post route, for this you would need to create a type with DTO 
	2. **@controller('items')**
	3. **@Req req: Request**
	4. **@Res res: Response**
	5. **@Param('id')**
	6. 
2. **DTO**
3. **Services**
	1. 


`nest g service item`

---

### install the cli
```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

#### main.ts
Server configrations.

#### app.module
Entry point.
```ts
import { Module } from '@nestjs/common';
import { StudentsModule } from '../student/student.module';
import { TeacherModule } from '../teacher/teacher.module';
  
@Module({
	imports: [StudentsModule, TeacherModule]
})

export class AppModule {}
```

#### Separate modules
```tsx
import { Module, NestModule, MiddlewareConsumer, RequestMethod } from '@nestjs/common';
import { StudentController } from './student.controller';
import { StudentService } from './student.service';
import { ValidStudentMiddleware } from "../common/middlewares/validStudent.middleware"

@Module({
	controllers: [StudentController],
	providers: [StudentService],
	exports: [StudentService]
})

export class StudentsModule implements NestModule {
	configure(consumer: MiddlewareConsumer) {
		consumer.apply(ValidStudentMiddleware).forRoutes({
			path: 'students/:studentId',
			method: RequestMethod.GET
		});
		consumer.apply(ValidStudentMiddleware).forRoutes({
			path: 'students/:studentId',
			method: RequestMethod.PUT
		});
	}
}
```

#### controllers
```tsx
import { Controller, Get, Param, ParseUUIDPipe, } from '@nestjs/common';
import { FindTeacherResponseDto } from './dto/teacher.dto';
import { TeacherService } from './teacher.service';

@Controller('teachers')
export class TeacherController {
	constructor(private readonly teacherService: TeacherService){}

	@Get()
	getTeachers(): FindTeacherResponseDto[] {
		return this.teacherService.getTeachers()
	}

	@Get('/:teacherId')
	getTeacherById(
		@Param('teacherId', new ParseUUIDPipe()) teacherId: string
	): FindTeacherResponseDto {
		return this.teacherService.getTeacherById(teacherId)
	}
}
```

#### providers/services
```ts
import { Injectable } from '@nestjs/common';
import { teachers } from '../db';
import { FindTeacherResponseDto } from './dto/teacher.dto';

@Injectable()
export class TeacherService {
	private teachers = teachers

	getTeachers(): FindTeacherResponseDto[] {
		return this.teachers
	}

	getTeacherById(id: string): FindTeacherResponseDto {
		return this.teachers.find(teacher => {
			return teacher.id === id
		})
	}
}
```

#### Decorators.
1. @params
2. @body
3. @Get, @put, @Controller, @Body & @Injectabe.

#### pipes
- transform
- validate

#### export and import services in modules.
```tsx
import { Module } from '@nestjs/common';
import { StudentsModule } from '../student/student.module';
import { StudentTeacherController } from './student.controller';
import { TeacherController } from './teacher.controller';
import { TeacherService } from './teacher.service';

@Module({
	imports: [StudentsModule],
	controllers: [TeacherController, StudentTeacherController],
	providers: [TeacherService]
})

export class TeacherModule {}
```
