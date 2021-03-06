# NestJS DygmaRaiseApi
A package for NestJS to comunicate with Dygma Raise

# Usage
app.module.ts:
```
import { Module } from '@nestjs/common';
import { DygmaModule } from 'nestjs-dygmaraiseapi';
import { AppService } from './app.service';

@Module({
	imports: [DygmaModule.register({ portName: 'COM3' })],
	providers: [AppService],
})
export class AppModule {}
```

main.ts:
```
import { NestFactory } from '@nestjs/core';
import { LedControllService } from 'nestjs-dygmaraiseapi';
import { AppModule } from './app.module';
import { Color } from 'nestjs-dygmaraiseapi';

async function bootstrap(): Promise<void> {
	const app = await NestFactory.create(AppModule);
	const ledControllService = app.get(LedControllService);

	ledControllService.setLeds(
		new Color({ red: 255, blue: 0, green: 0 }),
		ledControllService.getLedMap('backlight').ledIds,
	);
}
bootstrap();
```