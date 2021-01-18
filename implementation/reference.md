## Optimizations

### Replacing _momentum_optimizer_ with _adam_optimizer_

Update *pipeline_file.config* file with by replacing:

 `optimizer {
  momentum_optimizer: {
      learning_rate: {
        cosine_decay_learning_rate {
          learning_rate_base: 8e-2
          total_steps: 300000
          warmup_learning_rate: .001
          warmup_steps: 2500
        }
      }
      momentum_optimizer_value: 0.9
   }
    use_moving_average: false
  }`

With:

`optimizer {
    adam_optimizer: {
      learning_rate: {
        manual_step_learning_rate {
          initial_learning_rate: .0002
          schedule {
            step: 4500
            learning_rate: .0001
          }
          schedule {
            step: 7000
            learning_rate: .00008
          }
          schedule {
            step: 10000
            learning_rate: .00004
          }
        }
      }
    }
    use_moving_average: false
  }`
