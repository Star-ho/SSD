---
created: 2024-03-31T22:41:00
date: 2024-04-13T22:56
---
package team.hlab.infrastructure.jpa

import org.springframework.boot.autoconfigure.EnableAutoConfiguration
import org.springframework.boot.test.autoconfigure.jdbc.AutoConfigureTestDatabase
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest
import org.springframework.context.annotation.ComponentScan
import org.springframework.data.jpa.repository.config.EnableJpaAuditing
import org.springframework.test.context.ActiveProfiles
import org.springframework.test.context.ContextConfiguration

@ComponentScan
@EnableJpaAuditing
@EnableAutoConfiguration
private class SpringJpaTestConfiguration

@ActiveProfiles("local")
@ContextConfiguration(classes = [SpringJpaTestConfiguration::class])
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@DataJpaTest
annotation class SpringJpaTest

#Spring-boot
#Test  